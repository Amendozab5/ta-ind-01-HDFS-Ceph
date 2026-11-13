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
