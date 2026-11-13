# TA-IND-01 — Informe Académico Individual

**Análisis crítico comparativo: HDFS frente a Ceph**
*Dos filosofías de almacenamiento distribuido: metadatos centralizados vs. colocación determinista*

| Campo | Valor |
|---|---|
| Universidad | Universidad Técnica Estatal de Quevedo (UTEQ) |
| Facultad | Facultad de Ciencias de la Ingeniería |
| Carrera | Ingeniería en Software / Computación |
| Asignatura | Sistemas Distribuidos |
| Código | TA-IND-01 |
| Estudiante | _Angello Agustin Mendoza Bermello_ |
| Paralelo | _7mo B_ |
| Fecha | Noviembre 2026 |
| Repositorio | _https://github.com/Amendozab5/ta-ind-01-HDFS-Ceph_ |
| Video de sustentación | _completar enlace (YouTube no listado o Drive abierto)_ |

## Compilación

- **Compilador:** pdfLaTeX (TeX Live 2024 o MiKTeX actualizado).
- **Archivo principal:** `informe/main.tex`
- **Orden de comandos:**

```bash
cd informe
pdflatex main.tex
biber main
pdflatex main.tex
pdflatex main.tex
```

- **Dependencias:** `biblatex` con estilo `ieee`, `biber`, `tikz`, `pgfplots`, `booktabs`, `graphicx`, `hyperref`, `csquotes`, `caption`, `geometry`, `fancyhdr`.

## Estructura del repositorio

```
.
├── README.md
├── BITACORA.md              # bitácora fechada de sesiones
├── referencias.bib          # fuentes en formato BibLaTeX (estilo IEEE)
├── fuentes/                 # ficha de cada artículo (DOI, licencia, enlace)
├── informe/                 # código LaTeX y PDF compilado
├── figs/                    # diagrama de arquitectura (TikZ/draw.io)
├── capturas/                # evidencias: ejecución, lectura de fuentes, experimento
├── experimento/             # comandos y salidas del experimento (docker-compose, logs)
└── sga/                     # PDF de una página para el SGA
```

## Estado del trabajo

- [x] Tema definido y delimitado (HDFS vs Ceph).
- [x] Corpus inicial de fuentes reunido y verificado (DOI + acceso abierto).
- [ ] Levantamiento del clúster HDFS y capturas de ejecución.
- [ ] Experimento de tolerancia a fallos.
- [ ] Redacción y compilación del informe.
- [ ] Video de sustentación.
