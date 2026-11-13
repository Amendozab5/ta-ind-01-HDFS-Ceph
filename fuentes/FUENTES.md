# Fuentes del informe

Registro de cada fuente: datos bibliográficos, DOI y estado de descarga del PDF.
Los PDF se guardan fuera del repositorio (carpeta local `artículos científicos/`) para no
versionar material de terceros; aquí queda la ficha verificable de cada uno.

| # | Autor(es) | Año | Revista | DOI | Licencia OA | PDF |
|---|---|---|---|---|---|---|
| 1 | Lee, Akella, Bateni, Lin, Lohstroh, Menard | 2023 | ACM TECS 22(5s) | 10.1145/3609119 | CC-BY | Sí (preprint arXiv) |
| 2 | Ahmed, Karpenko, Tarasyuk, Gorbenko, Sheikh-Akbari | 2023 | Radioelectron. Comput. Syst. (2) | 10.32620/reks.2023.2.14 | CC-BY-NC | Sí |
| 3 | Myrhorodskyi, Romanyuk | 2025 | Inf. Technol. Comput. Eng. (22) | 10.31649/vitce/3.2025.101 | CC-BY | Pendiente (landing) |
| 4 | Kim | 2021 | Applied Sciences 11(8) | 10.3390/app11083298 | CC-BY | Sí |
| 5 | Dhulavvagol, Totad | 2023 | Procedia CS 218 | 10.1016/j.procs.2023.01.254 | Diamond OA | Pendiente (bloqueo) |
| 6 | — | 2023 | IEEE Access 11 | 10.1109/ACCESS.2023.3247190 | CC-BY | Sí |
| 7 | Chum, Park, Choi | 2021 | Electronics 10(7) | 10.3390/electronics10070847 | CC-BY | Sí |
| 8 | Li, Wang | 2023 | Cluster Computing 26(2) | 10.1007/s10586-022-03764-3 | CC-BY | Sí |
| 9 | Anagnostakis, Glavas | 2025 | Future Internet 17(4) | 10.3390/fi17040157 | CC-BY | Sí |
| 10 | Lei, Chen, Wang, Yang | 2024 | Electronics 13(3) | 10.3390/electronics13030593 | CC-BY | Sí |

## Verificación aplicada

1. Metadatos (autores, año, título, revista, volumen, número, páginas) consultados en la API de Crossref.
2. Estado de acceso abierto y licencia consultados en la API de Unpaywall.
3. Descarga comprobando cabecera `%PDF` (no página HTML de error).
4. Identidad confirmada leyendo la primera página del PDF con `pypdf`.

## Nota sobre la fuente 1

El PDF descargado es el preprint de arXiv (`arXiv:2301.08906`), cuyo título dice
"…in Distributed **Real-Time** Systems". La versión publicada en ACM TECS se titula
"…in Distributed **Cyber-Physical** Systems". Se cita siempre la versión publicada con su DOI.
