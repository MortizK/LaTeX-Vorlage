# Projektarbeit II

Dies ist ein LaTeX-Template für wissenschaftliche Arbeiten an der DHBW. Es ist bewusst schlank gehalten und nutzt nur die bereits vorhandene Projektstruktur und die in der Preamble eingebundenen Pakete.

## Projektstruktur

- [main.tex](main.tex) ist die zentrale Einstiegsdatei.
- [preamble.tex](preamble.tex) lädt die verwendeten Pakete und globale Formatierung.
- [settings.tex](settings.tex) enthält die Metadaten für Titel, Autor, Studiengang und Partner.
- [chapters/allChapters.tex](chapters/allChapters.tex) steuert die Reihenfolge der Kapitel.
- [chapters/](chapters/) enthält die einzelnen Kapiteldateien.
- [other/](other/) enthält Frontmatter wie Titelseite, Sperrvermerk, Eigenständigkeitserklärung, Abstract und Glossar.
- [images/](images/) ist der Standardordner für Abbildungen.
- [literatur.bib](literatur.bib) ist die Literaturdatenbank.

## Kompilieren

Für VS Code mit LaTeX Workshop ist diese Reihenfolge vorgesehen:

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

Wichtig: Nach Änderungen an Literatur, Glossar oder Abkürzungen ist meist mehr als ein Durchlauf nötig. Wenn Verweise oder Verzeichnisse nicht sofort stimmen, den kompletten Build noch einmal starten.

## So ist das Dokument aufgebaut

`main.tex` lädt zunächst die Einstellungen und danach die Kapitel. Die Reihenfolge ist bereits in [chapters/allChapters.tex](chapters/allChapters.tex) definiert. Neue Kapitel sollten dort ergänzt werden, damit sie automatisch im Dokument erscheinen.

Der Aufbau ist bewusst in Blöcke getrennt:

- Frontmatter in [other/](other/)
- Fließtext in [chapters/](chapters/)
- Abbildungen in [images/](images/)
- Quellen in [literatur.bib](literatur.bib)

## Verwendete Pakete und wie man sie nutzt

### Sprache und Layout

- `babel` mit `ngerman` steuert deutsche Silbentrennung und Bezeichnungen wie Inhaltsverzeichnis.
- `fontenc` und `inputenc` sorgen für korrektes UTF-8-Verhalten.
- `csquotes` ist für sprachabhängige Anführungszeichen und passt gut zu `biblatex`.

### Bilder und PDFs

- `graphicx` für Abbildungen mit `\includegraphics`.
- `pdfpages` für komplette PDF-Seiten mit `\includepdf`.

Beispiel:

```latex
\begin{figure}[h]
    \centering
    \includegraphics[width=0.8\textwidth]{mein-bild.png}
    \caption{Beispielabbildung}
    \label{fig:beispiel}
\end{figure}
```

### Tabellen

- `array`, `tabularx` und `multirow` sind für Tabellen vorgesehen.
- Nutze `tabularx`, wenn eine Tabelle automatisch auf die Textbreite angepasst werden soll.

Beispiel:

```latex
\begin{table}[h]
    \centering
    \label{tab:beispiel}
    \begin{tabularx}{\textwidth}{l X}
        \hline
        Spalte 1 & Spalte 2 \\
        \hline
        A & Langer Text, der umbrechen darf. \\
        \hline
    \end{tabularx}
    \caption{Beispieltabelle}
\end{table}
```

### Code

- `listings` für Quellcode.
- In der Preamble sind bereits `Python` und `HTML` geladen.
- Zeilenumbrüche sind aktiviert, dadurch werden längere Codezeilen besser verarbeitet.

Beispiel:

```latex
\begin{lstlisting}[language=Python, caption={Beispielcode}]
def greet(name):
    print(f"Hallo, {name}!")
\end{lstlisting}
```

### Literatur

- `biblatex` mit `biber` verwaltet die Quellen aus [literatur.bib](literatur.bib).
- Zitate erfolgen mit `\cite{schluessel}`.
- Das Literaturverzeichnis wird mit `\printbibliography` ausgegeben.

Beispiel:

```latex
Ein Verweis auf eine Quelle \cite{alhamadi2025behavioural}.
```

### Glossar und Abkürzungen

- `glossaries` verwaltet Glossarbegriffe und Abkürzungen.
- Neue Einträge kommen in [other/glossary.tex](other/glossary.tex).
- Im Text werden Einträge mit `\gls{schluessel}` verwendet.

Beispiel:

```latex
\newacronym{hci}{HCI}{Human-Computer Interaction}
\newglossaryentry{cosmos}
{
        name=COSMOS,
        description={Eine Webapplikation der T-Systems zur Verwaltung von Cloud-Ressourcen}
}
```

Im Text dann:

```latex
\gls{hci}
\gls{cosmos}
```

### Querverweise und Links

- `hyperref` erzeugt klickbare Links im PDF.
- Mit `\label{...}` und `\ref{...}` kannst du auf Kapitel, Abbildungen und Tabellen verweisen.
- Für einen direkten Link auf eine Seite oder einen Abschnitt kannst du ebenfalls `\ref` oder `\autoref` nutzen, falls du es im Dokument einheitlich halten willst.

Beispiel:

```latex
Wie in Abbildung \ref{fig:beispiel} gezeigt ...
```

## Metadaten pflegen

Die Angaben für Titel, Autor, Matrikelnummer, Studiengang, Partner und Betreuer stehen in [settings.tex](settings.tex). Diese Datei ist die zentrale Stelle, wenn du nur die Kopfdaten ändern willst.

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

## Typische Fehler und wie man damit umgeht

### Overfull \hbox / hbox to wide!

Diese Meldung bedeutet, dass LaTeX eine Zeile oder Box nicht sauber umbrechen konnte und über den Satzspiegel hinausläuft. Das ist kein Laufzeitfehler, aber ein Hinweis auf ein Layoutproblem.

Typische Ursachen:

- sehr lange Wörter oder zusammengesetzte Begriffe
- lange URLs, Dateinamen oder Querverweise
- zu breite Tabellen oder Bilder
- unpassende manuelle Zeilenumbrüche

Typische Lösungen:

- Text kürzen oder umformulieren
- lange Begriffe an sinnvoller Stelle trennen
- URLs mit `\url{...}` setzen statt als normaler Text
- Tabellen auf `tabularx` umstellen
- Bilder mit `width=...\textwidth` skalieren
- Codeblöcke bei Bedarf mit kleinen, gezielten Anpassungen umbrechen

Wenn die Meldung nur vereinzelt auftritt und der Text im PDF optisch noch sauber aussieht, kann sie manchmal toleriert werden. Wenn sie aber mehrfach vorkommt, sollte die betroffene Stelle angepasst werden.

### Unterfull / schlechte Umbrüche

Wenn Absätze oder Tabellen optisch unruhig wirken, ist meist der Inhalt oder die Spaltenbreite das Problem. Dann hilft es oft, den Text zu kürzen, die Tabelle anders zu strukturieren oder eine flexiblere Spaltenart zu verwenden.

### Literatur, Glossar oder Abkürzungen erscheinen nicht

Wenn Verweise fehlen oder leer bleiben:

1. alle Hilfsdateien neu erzeugen lassen
2. die Build-Reihenfolge komplett ausführen
3. die Schlüssel in [literatur.bib](literatur.bib) und [other/glossary.tex](other/glossary.tex) prüfen

### Kapitel oder Abbildungen werden nicht gefunden

- Prüfe den Pfad in `\input{...}` oder `\includegraphics{...}`.
- Achte darauf, dass die Datei wirklich im angegebenen Ordner liegt.
- Bei Bildern ist der Standardpfad bereits auf [images/](images/) gesetzt.

## Kurzablauf beim Schreiben

1. Inhalt in der passenden Kapiteldatei unter [chapters/](chapters/) ergänzen.
2. Bei Bedarf neue Bilder in [images/](images/) ablegen.
3. Quellen in [literatur.bib](literatur.bib) eintragen und mit `\cite{...}` verknüpfen.
4. Glossarbegriffe und Abkürzungen in [other/glossary.tex](other/glossary.tex) anlegen.
5. Mit der vollständigen Build-Reihenfolge kompilieren.
