# Wissenschaftliche Arbeiten in LaTeX

Dies ist ein LaTeX-Template für wissenschaftliche Arbeiten an der DHBW. Es ist bewusst schlank gehalten und von der [DHBW-Horb-Vorlage](https://github.com/dhbw-horb/latexvorlage) inspiriert.

## Projektstruktur

- [main.tex](main.tex) ist die zentrale Einstiegsdatei.
- [preamble.tex](preamble.tex) lädt die verwendeten Pakete und globale Formatierung.
- [settings.tex](settings.tex) enthält die Metadaten für Titel, Autor, Studiengang und Partner.
- [chapters/allChapters.tex](chapters/allChapters.tex) steuert die Reihenfolge der Kapitel.
- [chapters/](chapters/) enthält die einzelnen Kapiteldateien.
- [other/](other/) enthält Frontmatter wie Titelseite, Sperrvermerk, Eigenständigkeitserklärung, Abstract und Glossar.
- [images/](images/) ist der Standardordner für Abbildungen.
- [literature.bib](literature.bib) ist die Literaturdatenbank.

## Kompilieren

Für VS Code mit LaTeX Workshop ist diese Reihenfolge vorgesehen:

```bash
pdflatex main.tex
biber main
makeglossaries main
pdflatex main.tex
```

oder als Recipe im LaTeX Workshop:

```json
"latex-workshop.latex.recipes": [
    {
        "name": "pdflatex -> biber -> makeglossaries -> pdflatex",
        "tools": ["pdflatex", "biber", "makeglossaries", "pdflatex"]
    }
],
"latex-workshop.latex.tools": [
    {
        "name": "biber",
        "command": "biber",
        "args": ["%DOCFILE%"]
    },
    {
        "name": "makeglossaries",
        "command": "makeglossaries",
        "args": ["%DOCFILE%"]
    },
    {
        "name": "pdflatex",
        "command": "pdflatex",
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "%DOC%"
        ]
    }
]
```

## Quellen zum Nachlesen

Die wichtigsten Pakete in diesem Projekt haben offizielle Dokumentationen, die bei Detailfragen helfen. Am besten zuerst dort nachsehen, wenn ein Paketverhalten unklar ist.

- [KOMA-Script](https://ctan.org/pkg/koma-script) für die Dokumentklasse `scrreprt`
- [babel](https://ctan.org/pkg/babel) für Sprache, Silbentrennung und automatische Bezeichnungen
- [csquotes](https://ctan.org/pkg/csquotes) für sprachabhängige Anführungszeichen
- [graphicx](https://ctan.org/pkg/graphicx) für Abbildungen und Skalierung
- [pdfpages](https://ctan.org/pkg/pdfpages) für das Einbinden kompletter PDF-Seiten
- [float](https://ctan.org/pkg/float) für die erweiterte Platzierung von Gleitobjekten
- [xcolor](https://ctan.org/pkg/xcolor) für Farben
- [array](https://ctan.org/pkg/array), [tabularx](https://ctan.org/pkg/tabularx) und [multirow](https://ctan.org/pkg/multirow) für Tabellen
- [listings](https://ctan.org/pkg/listings) für Quellcode
- [biblatex](https://ctan.org/pkg/biblatex) und [biber](https://ctan.org/pkg/biber) für Literaturverwaltung
- [glossaries](https://ctan.org/pkg/glossaries) für Glossar und Abkürzungen
- [hyperref](https://ctan.org/pkg/hyperref) für klickbare Links und Verweise

Für allgemeine Einführungen sind außerdem die Pakethandbücher auf CTAN meist die beste Referenz. Dort stehen auch Beispiele, optionale Einstellungen und bekannte Einschränkungen.
