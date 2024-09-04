# LaTeX voor Beginners

**Georganiseerd door:** Filii Lamberti  
**Spreker:** Allyson Robert (PhD Studente)

Het doel van deze workshop is om studenten kennis te laten maken met LaTeX.

# Inhoud Workshop
- Vergelijkingen
- Figuren
- Tabellen
- Code snippets
- Referenties
- Delen van Projecten

# Inleiding

## Hoe ziet een LaTeX document eruit?

Een latex document bestaat uit een `*.tex` bestand. 
Dit wordt dan gecompileerd en produceert een PDF bestand.
Hieronder is een minimaal voorbeeld van zo een tex-bestand.

```latex
\documentclass{article}

\title{Oefening 1}
\author{Allyson Robert}
\date{\today}

\begin{document}
  \maketitle
  \tableofcontents
  \section{Introduction}
\end{document}
```

## Documentclass en Packages
- **Documentclass** definieert document type. Bijvoorbeeld:
  - `article`
  - `standalone`
  - `Uhphysreport`
- **Packages** voegen bijkomende functionaliteit toe aan jouw LaTeX document:
  - Voorbeelden: `amsmath`, `physics`, `graphicx`
  - Gebruik: `\usepackage{…}`
  - Onmiddellijk onder documentclass plaatsen
  - Volgorde is belangrijk, zo kan je best `hyperref` en `cleveref` als laatste inladen om conflicten te vermijden.
- **Environments** kan je toevoegen met begin en end:
  - `document` is de belangrijkste environment daar alles wat in je document moet verschijnen hierin zal staan
  - `figure`, `equation`, `align` zijn bijkomende voorbeelden waar in de workshop dieper op in wordt gegaan
- **Andere** 
  - title, author en date definieren enkele invulbare gegevens van je document
  - \maketitle en \tableofcontents zorgen ervoor dat een titel en inhoudstafel aangemaakt worden in de PDF versie
  - \section start een nieuw onderdeel van je tekst met een titel
  - 

## Overleaf: Geen Installatie Nodig
LaTeX gebruiken is nog nooit zo gemakkelijk geweest.
Je kan een online editor gebruiken waardoor je niets hoeft installeren.
De meest gebruikte editor is momenteel [www.overleaf.com](https://www.overleaf.com) en heeft vele voordelen.
- UHasselt students get free premium membership
- Cloud access to projects
- Many useful resources and tutorials
- Collaboration possible
- Let Op: Gebruik steeds de code editor, zo heb je controle over wat er gebeurt

Let wel op dat Overleaf zeer gebruiksvriendelijk wilt zijn en dus een groot aandeel veelgemaakte fouten detecteert en achter de schermen verbeterd.
Je kan het aantal errors zien in de editor, hou deze in het oog en verbeter ze zelf vooraleer de problemen te hoog opstapelen en onhandelbaar worden.

# Vergelijkingen

## Formules in de tekst
- Gebruik mathmode door gebruik van `\(…\)` of `$…$`.
  - `$x^2 + y^2 = c^2$`
  - `\(x^2 + y^2 = c^2\)`
- Gemakkelijk voor korte formules.
- Voorbeelden van Griekse letters en andere symbolen:
  - `\kappa`
  - `\hbar`
- Gebruik Detexify (App) voor het vinden van symbolen.

## Formules in blokken
```latex
\usepackage{amsmath}
…
\begin{align}
  \sum \vec{F} = 0 &\Rightarrow \vec{v} = \text{cte}\\
  %
  \vec{a} &= \frac{\sum \vec{F}}{m} \\
  %
  \vec{F}_{A\to B} &= -\vec{F}_{B \to A}
\end{align}
```

# Figuren

In een verslag ga je bijna altijd figuren willen toevoegen. Er bestaan twee soorten figuren:
- **Vectortekeningen** zijn ideaal omdat deze exact gedefinieerd worden door geometrie:
  - Gebruik illustrator of inkscape
  - Eerst exporteren naar PDF.
- **Bitmap** bestanden kunnen ook maar schalen niet doordat deze uit pixels bestaan. Gebruik hiervoor
  - PNG
  - JPEG (Standaard lossy compression)
Indien je kan werken met vectortekeningen is dit de beste keuze. Zo zien jouw figuren er altijd proper uit.

## Figure Environment

Wil je een figuur toevoegen aan jouw document dan kan dit met de `figure` environment die met de `graphicx` package beschikbaar is.
```latex
\usepackage{graphicx}
\usepackage{float}
…
\begin{figure}[H]
  \centering
  \includegraphics[width=\textwidth]{img/pikachu_transparent.png}
  \caption{Fat Pikachu is best Pikachu}
  \label{fig:pikachu}
\end{figure}
```
Merk op dat er in dit voorbeeld een caption en label aanwezig zijn.
Je figuren dienen in verslagen steeds een woordje uitleg te bevatten om de lezer te begeleiden bij het interpreteren van de figuur.
Zie ook dat er gebruik gemaakt is van de `float` package, deze zorgt ervoor dat figuren exact staan waar je ze wil.

## Minipages
Wil je meerdere figuren naast of onder elkaar plaatsen dan is de `minipage` package wat je zoekt.
Je kan ook `subfigures` gebruiken maar die geeft minder controle. 
Hier is een voorbeeld voor twee zij-aan-zij figuren.


  ```latex
  \begin{minipage}{0.45\textwidth}
  …
  \end{minipage}
  \hspace{0.05\textwidth}
  \begin{minipage}{0.45\textwidth}
  …
  \end{minipage}
  ```

## TikZ Ultimate Power (advanced users only)
Voor de meer gevorderde gebruikers biedt LaTeX een krachtige tool genaamd TikZ, waarmee je dynamisch afbeeldingen kunt tekenen. Dit heeft als voordeel dat de stijl van de afbeeldingen consistent blijft met de rest van je document, wat zorgt voor een uniforme en professionele uitstraling.

Om gebruik te maken van deze functionaliteit, moet je het TikZ package inladen in je LaTeX-document. Een handige manier om complexe figuren te creëren is door gebruik te maken van Geogebra 5. Met Geogebra kun je eenvoudig tekeningen maken en deze vervolgens exporteren als PGF/TikZ-code, die je direct in je LaTeX-document kunt opnemen.

Een belangrijk aandachtspunt bij het gebruik van TikZ is dat het snel zwaar kan worden om te compileren, vooral bij complexe tekeningen. Dit kan leiden tot langere wachttijden bij het genereren van je document. Mocht je echter hulp nodig hebben bij het genereren van TikZ-code, kan ChatGPT je ook hierbij ondersteunen. ChatGPT kan codevoorbeelden geven en je begeleiden bij het maken van complexe diagrammen en tekeningen in TikZ.

# Tabellen

Naast figuren zal je ook regelmatig nood hebben aan tabellen, deze kunnen heel omslachtig zijn om te maken.
Je hebt er de `tabular` en `tables` environments voor nodig.
De eerste helpt je met de inhoud van de tabel, terwijl de tweede je helpt om dit te verwerken in je tekst.
Zo kan je aan jouw tabel een caption toevoegen en deze centreren in het blad.

## Structuur van een Tabel
```latex
\usepackage{tabularx}
...
\begin{table}[!htpb]
  %
  \centering
  \caption{Example of a table}
  \label{tab:example_tab}
  %
  \begin{tabular}{|l|r|c|}
    \hline
    a & b & c \\ \hline
    1 & 2 & 3 \\ \hline
  \end{tabular}
  %
\end{table}
```

## Tabellen Makkelijk Maken
Tabellen maken kan heel vervelend zijn, gelukkig zijn er tools om dit gemakkelijk te maken. Zo is er [www.tablesgenerator.com](https://www.tablesgenerator.com).
- Navigeer naar [www.tablesgenerator.com](https://www.tablesgenerator.com).
- Maak je tabel of plak deze uit een excel-document
- Genereer de code
- Kopieer en plak deze code naar Overleaf
- Gebruik hier eventueel de Visual Editor om de tabel wat aan te passen.

# Code Snippets
Voor de informatici onder ons, en de toekomstige computationele wiskundige/fysici, is het altijd nuttig om stukjes code in een document te kunnen plaatsen.
Ook dit kan, hiervoor gebruikt je bijvoorbeeld de `listings` package.
Hier is een voorbeeld.

```latex
\usepackage{listings}
…
\begin{lstlisting}[language=Python,label=listing:python,caption=Python example with caption and label]
import webbrowser
def open_youtube_video():
    url = "https://www.youtube.com/watch?v=dQw4w9WgXcQ"
    webbrowser.open(url)
open_youtube_video()
\end{lstlisting}
```

Merk op dat de `verbatim` package en environment van dezelfde naam je toelaten om alles letterlijk te laten plaatsen in het document.

# Referenties

## Verwijzen naar vergelijkingen of figuren
Referenties in LaTeX worden beheerd met behulp van de `hyperref` en `cleveref` packages. 
Om een object zoals een vergelijking, figuur, of sectie te refereren, voeg je eerst een label toe met `\label{}`. 
Gebruik `\ref{}` of `\cref{}` om daarna naar dit object te verwijzen in je tekst. 
De  `cleveref` package zorgt ervoor dat LaTeX automatisch het type referentie (zoals "Figuur" of "Vergelijking") herkent en correct weergeeft. 
Dit maakt het eenvoudig om consistente en duidelijke verwijzingen in je document te creëren.

```latex
\usepackage[colorlinks=true]{hyperref}
\usepackage{cleveref}
…
```
- **Volgorde belangrijk!**
- `\label{eq:pythagoras}`
  - Gebruik eq/fig/sec/lst/... om labels te onderscheiden.
- `\cref{eq:pythagoras}`
  - Herkent type referentie volgens plaats label.

## Bibliografie

De bibliografie in LaTeX wordt beheerd met de `biblatex` package. 
Je kunt eenvoudig referenties toevoegen door een `.bib`-bestand aan te maken waarin je bronnen staan. Voeg dit bestand toe aan je document met `\addbibresource{references.bib}`. 
Om de bibliografie weer te geven, gebruik je `\printbibliography` waar je de lijst wilt laten verschijnen. 
Gebruik `\cite{}` om naar specifieke bronnen te verwijzen in je tekst. Dit maakt het eenvoudig om consistent en automatisch verwijzingen te beheren en een professioneel ogende literatuurlijst te genereren.

```latex
\usepackage{biblatex}
\addbibresource{references.bib}
...
\printbibliography
```

Voorbeeld:

```latex
@online{Overleaf,
title = {Learn LaTeX},
author = {Overleaf},
url = {https://www.overleaf.com},
urldate = {2023-09-24}
}
```

# Delen van Projecten
Het delen van LaTeX-projecten kan eenvoudig via platforms zoals Overleaf. 
Om een project te delen, kun je het project exporteren als een `.zip`-bestand via het menu "Download → Source". 
Dit bestand kan vervolgens worden geüpload naar een nieuw Overleaf-project door te kiezen voor "New Project → Upload Project". 
Om samen te werken, kun je het project delen door een e-mailadres in te voeren onder "Share". 
Hiermee kunnen meerdere gebruikers tegelijkertijd aan hetzelfde document werken, wijzigingen bijhouden en verschillende versies beheren via de geschiedenisfunctie.

## Projecten Importeren/Exporteren

- **Overleaf**: Menu → Download → Source.
- **Overleaf**: New Project → Upload Project → Upload .zip → Kies naam.

## Samenwerken aan een project

- **Overleaf**: Project → Share → Typ e-mail.
- Simultaan werken, reviewen, en versiegeschiedenis bijhouden.

# Miscellaneous
Hier zijn nog enkele tips die je kan gebruiken in je LaTeX carriere.

- Houd projecten foutloos.
- Let op onder/overfull `\hbox` waarschuwingen; vaak onschadelijk.
- Begin elke zin op een nieuwe regel.
- Voeg een lege regel toe in block equations door deze te kommentariëren met `%`.
- Undefined control sequence → waarschijnlijk een ontbrekende package.
- Wees voorzichtig met copy-paste.
- Maak goed gebruik van mappen en submappen.
- Organiseer afbeeldingen/hoofdstukken/etc.
- Zet je geladen packages in een `preamble.tex` bestand en laad dit met `\input{preamble}`.

## Fysica studenten: Template voor Verslagen

- Gemaakt volgens de richtlijnen.
- Veel packages zijn al voorgeladen.
- Bij problemen: allyson.Robert@uhasselt.be.

## Handige links
1. Overleaf: [https://www.overleaf.com](https://www.overleaf.com)  
   Online LaTeX-editor

2. Learn Overleaf: [https://www.overleaf.com/learn](https://www.overleaf.com/learn)  
   Algemene LaTeX-resource

3. Mathematical Expressions: [https://www.overleaf.com/learn/latex/Mathematical_expressions](https://www.overleaf.com/learn/latex/Mathematical_expressions)  
   Uitleg over vergelijkingen

4. Figures, Subfigures, and Tables: [https://www.overleaf.com/learn/latex/How_to_Write_a_Thesis_in_LaTeX_(Part_3)%3A_Figures%2C_Subfigures_and_Tables](https://www.overleaf.com/learn/latex/How_to_Write_a_Thesis_in_LaTeX_(Part_3)%3A_Figures%2C_Subfigures_and_Tables)  
   Uitleg over tabellen en figuren

5. UHasselt Physics Report Template: [https://github.com/Allyson-Robert/UHasselt_Physics_Report](https://github.com/Allyson-Robert/UHasselt_Physics_Report)  
   Fysica verslagtemplate

6. Filii LaTeX Workshop: [https://github.com/Allyson-Robert/filii-latex](https://github.com/Allyson-Robert/filii-latex)  
   Workshopmateriaal

7. Tables Generator: [https://www.tablesgenerator.com](https://www.tablesgenerator.com)  
   Tabelgenerator

8. Detexify (App)**: [https://detexify.kirelabs.org/classify.html](https://detexify.kirelabs.org/classify.html)  
   Identificeer LaTeX-symbolen

Deze lijst biedt handige links met korte uitleg voor elk aspect van de LaTeX-workshop en andere relevante bronnen.

Veel succes met je LaTeX projecten!

---
<sup>Last edited: September 4th, 2024<sup>
