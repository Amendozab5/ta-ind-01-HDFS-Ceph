# Fuentes del informe

Registro de cada fuente: datos bibliográficos, DOI y estado del PDF.
Los PDF no se versionan en el repositorio; quedan en la carpeta local
`artículos científicos/` y en la copia de lectura `TA-IND-01-fuentes/`.

Las entradas 01 a 14 corresponden al nombre del archivo de cada PDF.

| # | Autor(es) | Año | Revista | DOI | Licencia OA | PDF |
|---|---|---|---|---|---|---|
| 01 | Lee, Akella, Bateni, Lin, Lohstroh, Menard | 2023 | ACM TECS 22(5s) | 10.1145/3609119 | CC-BY | Sí (preprint arXiv) |
| 02 | Ahmed, Karpenko, Tarasyuk, Gorbenko, Sheikh-Akbari | 2023 | Radioelectron. Comput. Syst. 2(106) | 10.32620/reks.2023.2.14 | CC-BY-NC | Sí |
| 03 | Myrhorodskyi, Romanyuk | 2025 | Inf. Technol. Comput. Eng. 22(3) | 10.31649/vitce/3.2025.101 | CC-BY | Sí (sin capa de texto) |
| 04 | Kim | 2021 | Applied Sciences 11(8) | 10.3390/app11083298 | CC-BY | Sí |
| 05 | Dhulavvagol, Totad | 2023 | Procedia CS 218 | 10.1016/j.procs.2023.01.254 | Diamond OA | Sí (sin capa de texto) |
| 06 | Ahmed, Khafagy, Shaheen, Kaseb | 2023 | IEEE Access 11 | 10.1109/ACCESS.2023.3247190 | CC-BY | Sí |
| 07 | Chum, Park, Choi | 2021 | Electronics 10(7) | 10.3390/electronics10070847 | CC-BY | Sí |
| 08 | Li, Wang | 2023 | Cluster Computing 26 | 10.1007/s10586-022-03764-3 | CC-BY | Sí |
| 10 | Anagnostakis, Glavas | 2025 | Future Internet 17(4) | 10.3390/fi17040157 | CC-BY | Sí |
| 11 | Lei, Chen, Wang, Yang | 2024 | Electronics 13(3) | 10.3390/electronics13030593 | CC-BY | Sí |
| 12 | Lei, Wang, Chen, Yang | 2024 | Symmetry 16(6) | 10.3390/sym16060672 | CC-BY | Sí |
| 14 | Tchaye-Kondi, Zhai, Lin, Zhu, Tao, Yang | 2019 | arXiv:1903.05838 | 10.48550/arXiv.1903.05838 | arXiv | Sí |

## Verificación aplicada

1. Metadatos (autores, año, título, revista, volumen, número, páginas) consultados en la API de Crossref.
2. Estado de acceso abierto y licencia consultados en la API de Unpaywall.
3. Descarga comprobando cabecera `%PDF` (no página HTML de error).
4. Identidad confirmada leyendo la primera página del PDF, con `pypdf` cuando hay capa de texto y con un renderizador cuando el PDF es imagen.

## Uso en el informe

Once de las doce fuentes se citan en el documento; la 03 queda en reserva para
la sección de CAP y PACELC. La 14 es de 2019, fuera de la ventana de cinco años
que pide la consigna: se usa solo para el detalle de comunicación cliente–servidor
y del factor de replicación por defecto.

## Notas sobre dos archivos

- **03 y 05 no tienen capa de texto.** Son PDF de imagen: no admiten búsqueda ni
  subrayado hasta pasarles OCR. El contenido se leyó renderizando las páginas.
- **El PDF de la fuente 01 es el preprint de arXiv** (`arXiv:2301.08906`), cuyo título
  dice "…in Distributed **Real-Time** Systems". La versión publicada en ACM TECS se
  titula "…in Distributed **Cyber-Physical** Systems". Se cita siempre la versión
  publicada con su DOI.
