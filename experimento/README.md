# Experimento: tolerancia a fallos en HDFS

**Objetivo.** Provocar la caída de un DataNode y observar cómo reacciona HDFS:
detección del fallo, degradación de la replicación y recuperación.

**Hipótesis.** Con factor de replicación 3 y 3 DataNodes, la caída de uno deja los
bloques en estado `UNDER-REPLICATED`; el clúster sigue sirviendo lecturas (los datos
están en las otras dos réplicas) pero no puede volver a 3 copias hasta que el nodo
regrese. Es decir: **el plano de datos prioriza disponibilidad, el de metadatos no**.

## Requisitos

- Docker Desktop con contenedores Linux.
- 4 GB de RAM libres.

## Sobre los tiempos de detección

El `docker-compose.yml` incluye `dfs.heartbeat.interval=3` y
`dfs.namenode.heartbeat.recheck-interval=2000`, con lo que la detección del
fallo tarda unos 35 segundos.

En la corrida documentada en `salidas/` esos valores todavía no estaban
aplicados: el clúster se había levantado antes del cambio, así que usó los
valores por defecto. Por eso el último contacto de `dn2` figura a las
02:41:39 UTC y la declaración de muerte a las 03:01:47 UTC, unos 20 minutos.
La fórmula teórica con valores por defecto es 2 × 5 min + 10 × 3 s = 10 min 30 s;
el tiempo observado fue mayor porque a ese umbral se suma el ciclo periódico
de comprobación del NameNode.

## Puesta en marcha

```bash
docker compose up -d
docker compose ps
```

Esperar ~40 s y comprobar el NameNode en <http://localhost:9870>.

## Guion del experimento

| Paso | Comando | Qué debe verse |
|---|---|---|
| 1 | `docker exec -it nn hdfs dfsadmin -report` | 3 DataNodes vivos, capacidad total |
| 2 | `docker exec -it nn hdfs dfs -mkdir -p /uteq/<usuario>` | directorio creado |
| 3 | `docker cp datos.txt nn:/tmp/ && docker exec -it nn hdfs dfs -put /tmp/datos.txt /uteq/<usuario>/` | archivo subido |
| 4 | `docker exec -it nn hdfs fsck /uteq/<usuario>/datos.txt -files -blocks -locations` | 3 réplicas del bloque |
| 5 | `docker stop dn2` | el contenedor se detiene |
| 6 | `docker exec -it nn hdfs dfsadmin -report` | `Dead datanodes: 1` |
| 7 | `docker exec -it nn hdfs fsck / -files -blocks` | bloque `UNDER-REPLICATED` |
| 8 | `docker start dn2` y repetir el paso 7 | vuelve a 3 réplicas |

## Evidencia a capturar

Cada captura debe incluir el prompt con **usuario**, **hostname** y **fecha/hora** del equipo.

1. `docker compose ps` con los 4 contenedores en marcha.
2. `hdfs dfsadmin -report` con 3 DataNodes vivos.
3. `hdfs fsck ... -locations` mostrando las 3 réplicas.
4. `hdfs fsck /` con el bloque `UNDER-REPLICATED` tras `docker stop dn2`.
5. (Opcional) vuelta a estado saludable tras `docker start dn2`.

## Interpretación esperada

- **Detección:** el NameNode marca el DataNode como muerto tras ~10,5 min por defecto
  (`dfs.namenode.heartbeat.recheck-interval` × 2 + 10 × `dfs.heartbeat.interval`).
  Si se quiere ver rápido, reducir esos valores en el compose y documentarlo.
- **Disponibilidad:** las lecturas siguen funcionando desde las réplicas restantes.
- **Consistencia:** no hay riesgo de dato obsoleto porque los bloques son inmutables;
  el problema es de **durabilidad**, no de consistencia.
- **Recuperación:** la re-replicación consume ancho de banda y es la razón por la que
  HDFS no baja de 3 copias por defecto.
