# quarto-cv

This repository contains a [quarto](https://quarto.org) extension designed to generate a Curriculum Vitae (CV). Optionally, publication lists from a BibTeX file can be included. 

This extension is based on the [publicationlist](https://github.com/produnis/publicationlist) extension.


![](https://www.produnis.de/blog/posts/2021-04-19-publikationsliste-im-lebenslauf-mit-latex/publikationslebenslauf.png)

## Installation

To use this extension, execute the following command:

`quarto use template produnis/qaurto-cv`


## Usage
This extension uses the LaTeX document class "`moderncv`". Thus, all CV entries needs to be written in `LaTeX` code. Have a look at the example files coming with this extension for how to use them. In short,

- use `\cvline{KEY}{VALUE}` to create a new line entry, e.g. `\cvline{Name}{Albert Hastig}`.
- use `\cventry{DATE}{VALUE1}{VALUE2}{VALUE3}{VALUE4}{VALUE5}` to create a new time line entry, e.g. `\cventry{1967-2001}{Professor for Everything}{Muppet Show}{Sesame Street}{}{}`

You can edit the `moderncv` options in YAML with parameters

```
---
moderncvtheme: casual # classic #casual
cvoption: red  # green, red, orange, grey
---
```
### BibTeX file

This Quarto template takes a BibTeX file (e.g., `literatur.bib`) and generates a publication list. Examine the provided `literatur.bib` for reference.
If you don't want a publication list, comment out these lines in YAML:

```
---
#bibliography: literatur.bib
#subbibliography: true  # subheadings for bibliographies
#publikationen:
#  - list:
#      key: auswahl
#      title: Publikationen (Auswahl)
---
```

In order to create a `.bib` file, follow these steps:

- Organize your publications in [Zotero](https://www.zotero.org)
- Utilize the "Tags" tab in Zotero to categorize entries as journal articles, book chapters, or "gray literature." This categorization is essential for later differentiation in the publication list.
- Export the literature entries from Zotero as a "Bibtex" file (e.g., `literatur.bib`).
- Example Bibtex file structure:

```
@article{hastig1,
    title = {Regressionsmodelle für ordinale {Zielvariablen}},
    volume = {10},
    issn = {1860-9171},
    language = {de},
    number = {1},
    journal = {Journal der Zahlenkunde},
    author = {Hastig, Alber and Thefrog, Kermit},
   author+an = {1=highlight},
  year = {2014},
    keywords = {auswahl, journal, peer-reviewed},
    pages = {1--9}
}

@article{hastig2,
    title = {Warum bin ich so muede?},
    volume = {27},
    language = {de},
    number = {4},
    urldate = {2018-10-25},
    journal = {Journal der rhetorischen Fragen},
    author = {Schlappmann, Michael and ZuSpaet, Carmen and Hastig, Albert},
   author+an = {3=highlight},
  month = aug,
    year = {2014},
    keywords = {auswahl, journal, peer-reviewed},
    pages = {269--277}
}
```
Note the inclusion of keywords (tags) in each entry.

- Manually add the line  `author+an = {2=highlight}` to each author entry in the Bibtex file. This informs Quarto about your name's position in the author list (2 in this example), allowing it to highlight your name in bold during  `.tex` conversion. Though optional, this step enhances the presentation.

### YAML

In the YAML header, under the `publikationen` parameter, create a list entry for each keyword you wish to print. Specify the `key` as the keyword and `title` as the corresponding heading for that list. The example below illustrates printing four publication lists (for keywords "journal," "buch," "buchkapitel," and "konferenz"):

```
publikationen:
  - list:
      key: journal
      title: Zeitschriftenartikel (peer-reviewed)
  - list:
      key: buch
      title: Bücher   
  - list:
      key: buchkapitel
      title: Buchkapitel
  - list:
      key: konferenz
      title: Konferenzbeiträge (peer-reviewed) 
```

#### several bibliographies
If you have several bibliographies, you might want to switch the headings style with parameter `subbibliography: true`. This will create sub-headings for all lists. In this case, your `.qmd` file should end with

```
(... my CV entries ...)

# Publications (selection)
# do not remove me

```

See `example-multi-bib.qmd` as an example.

### Umlauts and ß

All Umlauts are supported, but for **ß** you must type `\ss` in your documents.

