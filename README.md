# TA-IND-01 — Informe Académico Individual

**Análisis crítico comparativo: HDFS frente a Ceph**
*Dos filosofías de almacenamiento distribuido: metadatos centralizados vs. colocación determinista*

| Campo | Valor |
|---|---|
| Universidad | Universidad Técnica Estatal de Quevedo (UTEQ) |
| Facultad | Facultad de Ciencias de la Ingeniería |
| Carrera | Ingeniería en Software |
| Asignatura | Sistemas Distribuidos |
| Código | TA-IND-01 |
| Estudiante | Angello Agustín Mendoza Bermello |
| Paralelo | 7mo B |
| Fecha | Noviembre 2026 |
| Repositorio | https://github.com/Amendozab5/ta-ind-01-HDFS-Ceph |
| Video de sustentación | pendiente |

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
├── experimento/             # comandos, compose y salidas del experimento
└── sga/                     # PDF de una página para el SGA
```

## Estado del trabajo

- [x] Tema definido y delimitado (HDFS vs Ceph).
- [x] Corpus de fuentes reunido y verificado (DOI + acceso abierto).
- [x] Clúster HDFS levantado y capturas de ejecución.
- [x] Experimento de tolerancia a fallos (caída y recuperación de un DataNode).
- [ ] Diagrama de arquitectura y esquema a mano (Anexo A).
- [ ] Redacción y compilación del informe.
- [ ] Capturas de lectura de fuentes (Anexo B).
- [ ] Video de sustentación.
