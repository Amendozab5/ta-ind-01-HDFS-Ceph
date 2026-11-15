# Bitácora de trabajo

Registro cronológico de sesiones. Cada entrada debe coincidir con la fecha de los commits.

---

## 2026-11-13 — Sesión 1: definición del tema y corpus de fuentes

**Tiempo dedicado:** 3 h 30 min

**Qué hice**

1. Revisé los sistemas ya elegidos por el curso para evitar duplicidad (Cassandra/MongoDB, Discord/Matrix, Kafka/RabbitMQ, etcd/ZooKeeper, CockroachDB/Spanner, Redis/Hazelcast, Kubernetes/Swarm, ClickHouse/Elasticsearch, Syncthing/Unison, NATS/Pulsar, InfluxDB/Prometheus, Consul/Eureka).
2. Detecté que la categoría *almacenamiento distribuido* estaba libre y elegí **HDFS** como sistema principal y **Ceph** como comparador, por el contraste metadatos centralizados vs. colocación determinista (CRUSH).
3. Reuní y verifiqué 10 artículos de acceso abierto: metadatos en Crossref, estado OA en Unpaywall, cabecera `%PDF` y lectura de la primera página para confirmar que el título correspondía.

**Problemas encontrados y cómo los resolví**

- `www.mdpi.com` devuelve HTTP 403 al descargar PDF de forma automatizada → usé el CDN directo `mdpi-res.com` con el patrón `d_attachment/<revista>/<revista>-<vol>-<art>/article_deploy/...`.
- `pip install pypdf` falla por permisos del sandbox en el directorio temporal → descargué el wheel desde la API de PyPI y lo descomprimí con `zipfile` en `_libs/`.
- ScienceDirect y Taylor & Francis bloquean la descarga automatizada → quedan 4 fuentes pendientes de descarga manual.

**Decisiones**

- El informe se centrará en CAP/PACELC aplicado a dos capas distintas de HDFS (metadatos CP vs. datos AP) y en la ausencia de palancas de consistencia en HDFS frente a `min_size` en Ceph.
- El experimento será: clúster HDFS de 1 NameNode + 3 DataNodes en Docker, matar un DataNode y observar `fsck` (UNDER-REPLICATED) y la re-replicación al reiniciarlo.

**Próxima sesión**

- Levantar el clúster, capturas 1 y 2, y primer borrador de la carátula e introducción.

---

## 2026-11-13 — Sesión 2: clúster, experimento y capturas

**Tiempo dedicado:** 3 h

**Qué hice**

1. Levanté un clúster de un NameNode y tres DataNodes con Docker Compose, red `hdfsnet` y un volumen con nombre por contenedor, y comprobé el NameNode en el puerto 9870.
2. Subí `datos.txt` a `/uteq/aamen/datos.txt` y verifiqué con `fsck` que el bloque tenía tres réplicas.
3. Detuve el contenedor `dn2` y documenté el estado degradado: dos DataNodes vivos, uno muerto y el bloque bajo replicación.
4. Comprobé que el archivo seguía siendo legible con un nodo caído.
5. Reinicié `dn2` y verifiqué en el `fsck` la vuelta a tres réplicas sin ninguna orden de reconstrucción.
6. Guardé las capturas y las salidas de los comandos en `capturas/` y `experimento/salidas/`, y publiqué todo en el repositorio.

**Problemas encontrados y cómo los resolví**

- La detección del fallo tardó unos 20 minutos y no los 10 min 30 s que predice el cálculo teórico. El clúster se había creado antes de añadir los intervalos de heartbeat al `docker-compose.yml`, así que corrió con los valores por defecto. Documenté la diferencia en `experimento/README.md` en vez de ocultarla.
- Durante la ventana en que el nodo estaba caído pero no declarado muerto, `hdfs dfs -cat` falló con `NullPointerException` porque Docker retira el nombre del contenedor detenido del DNS. Esa salida no servía como evidencia y no se usó.
- El primer `datos.txt` era una sola línea de 58 bytes y no identificaba el equipo ni la secuencia; lo reemplacé por un manifiesto de 1386 bytes y repetí el experimento completo, de modo que el tamaño del bloque en el `fsck` coincidiera con el del archivo declarado.
- El `git push` fue rechazado porque había un commit hecho desde la interfaz web del repositorio. Resolví con `git checkout -- .`, `git pull --rebase origin main` y `git push`.

**Decisiones**

- El indicador que documenta el riesgo no es `Status: HEALTHY` sino `Under-replicated blocks`, porque el archivo estuvo sano y a la vez con una réplica de menos.
- Las capturas se numeraron por el orden de la secuencia y no por el orden en que se tomaron, y se anotó en el `README` del experimento que la captura de tres réplicas se tomó tras la recuperación, no antes del fallo.

---

## 2026-11-14 — Sesión 3: diagrama de arquitectura y redacción del informe

**Tiempo dedicado:** 3 h

**Qué hice**

1. Dibujé el esquema de arquitectura a mano y lo pasé a `figs/arquitectura-hdfs-ceph.drawio`, con dos paneles: HDFS con el NameNode como plano de control y Ceph con los monitores y la colocación por CRUSH.
2. Separé en el diagrama los dos planos de HDFS, que en el boceto inicial estaban al mismo nivel, y marqué el DataNode caído.
3. Redacté `informe/main.tex` con la estructura completa: carátula, resumen, introducción, arquitectura, las cuatro secciones de la Unidad 1, experimentación, ejemplos del entorno, tabla comparativa, postura crítica, conclusiones, declaración de uso de IA y anexos.
4. Contrasté cada cifra del apartado de experimentación con las salidas archivadas en `experimento/salidas/`, y verifiqué que el identificador del bloque fuera el mismo en las tres capturas.
5. Revisé la redacción y el formato LaTeX con apoyo del asistente, y dejé la declaración de uso de inteligencia artificial de la sección correspondiente.

**Decisiones**

- El diagrama del informe va en TikZ, para que el PDF lo incluya como vector y no dependa de un archivo externo; el archivo `.drawio` queda en el repositorio como fuente editable.
- No inventé un incidente real de HDFS: en el corpus consultado no hay un post mortem verificable, así que el informe declara esa limitación y documenta el incidente reproducible propio.
- Los anexos A y B usan una comprobación de existencia del archivo de imagen, de modo que el documento compila aunque las capturas todavía no estén, y se incorporan solas cuando se añaden.

**Próxima sesión**

- Compilar el PDF y revisar el resultado.
- Fotografiar el esquema a mano y añadir las capturas de lectura de fuentes.
- Grabar el video de sustentación y preparar el PDF de una página para el SGA.

---

## 2026-11-15 — Sesión 4: cierre, video de sustentación y entrega

**Tiempo dedicado:** 2 h

**Qué hice**

1. Compilé el informe definitivo con pdflatex y iber, y verifiqué que los dos anexos aparecieran en su propia página con las imágenes incorporadas.
2. Pasé la redacción completa a tercera persona, sin cambiar el contenido, y reescribí el resumen para que quedara dentro del rango de 150 a 200 palabras y nombrara el sistema comparado.
3. Corregí la página de las citas del artículo de Ceph: la afirmación sobre los placement groups está en la página 1128, y la 1127 es la revisión de trabajos previos.
4. Recorté los márgenes de papel de la fotografía del esquema a mano y la incorporé al Anexo A, con el nombre y la fecha visibles.
5. Incorporé las tres capturas de lectura al Anexo B, cada una con el pie que indica autor, revista y página.
6. Grabé el video de sustentación explicando las capturas del experimento y lo subí a YouTube como no listado. El enlace quedó en el README.
7. Corregí en el README el nombre de la asignatura y el de la facultad, que no coincidían con la carátula ni con la página del SGA.

**Problemas encontrados y cómo los resolví**

- La bibliografía empezaba al final de la página de conclusiones y se partía por la mitad; añadí un salto de página antes para que ocupe una hoja completa.
- La captura del Anexo A se separaba de su pie de foto al compilar; encerré cada captura en un bloque indivisible.
- Repetir el experimento en vivo acercaba el video al límite de duración, así que se grabó explicando las capturas ya archivadas en lugar de ejecutar de nuevo el clúster.

**Decisiones**

- El video explica las capturas en el orden en que se produjeron y dedica la mayor parte del tiempo a la del estado degradado, que es la que sostiene la conclusión.
- El resumen menciona los cuatro conceptos de la unidad y las dos conclusiones, para que se entienda completo sin depender del resto del documento.

**Próxima sesión**

- Ninguna: el trabajo queda entregado.
