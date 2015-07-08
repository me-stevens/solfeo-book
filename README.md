# Solfeo Book
## A book to learn music notation

This book uses [MuseScore](http://musescore.org/) to generate the scores, and [LilyPond](http://lilypond.org) to typeset music notation in TeX. **MuseScore** is a free and open-source project to create, play and print music scores. **LilyPond** acts as a "preprocessor" for your TeX files and generates a TeX file with your TeX code plus the processed LilyPond commands. Then you can use your preferred TeX compiler to generate a PDF file. This project uses **XeLaTeX**.

To work in this document you need:

* **XeLaTeX**, which can be found in the `texlive-xetex` package.
* It also helps to install the packages in `texlive-latex-base`, `texlive-latex-recommended`, `texlive-latex-extra`, `texlive-fonts-extra` and `texlive-fonts-recommended`.
* **LilyPond**. Please go to [LilyPond download page](http://lilypond.org/download.html) and choose the file for your system. If, like me, you are using Ubuntu, you just need to download a `lilypond-VERSION.sh` file and then run `sh lilypond-VERSION.sh` in a terminal to install it.
* **MuseScore**. [Download it here](http://musescore.org/en/download). It makes editing easier, and allows nice blog embedding with play options out of the box.

### Workflow

The extension `mscz` refers to MuseScore files, while the extension `ly` refers to LilyPond files. Since the scores will also be used in the blog, and it is convenient to have them separated as individual files, they are first created in MuseScore, and then saved in `ly` format.  The `ly` and `mscz` files are stored in the `scores` folder.  

The `ly` files are then embedded in the `lytex` files using LilyPond's command `\lilypondfile`. The `lytex` extension tells LilyPond that it is a TeX file containing LilyPond commands. To compile `lytex` files use `lilypond-book` on your terminal. If you just want to compile the `ly` files, use `lilypond` instead.

The `lytex` files allow you to type text, paragraphs, headings, etc., as well as music, just as you would do it in a normal LaTeX document, while the `ly` files only support LilyPond syntax.

#### Setting MuseScore up

Be sure to have your MuseScore configured so that you use **A4 paper** with the left and right page margins set to **3cm** and the scale to **1.5**. Also, the font should be set to the one used in the book (Alegreya). You can do that in "**Layout > Page Settings...**" and "**Layout > Text Settings...**" or import the `MuseScoreStyle.mss` file provided in this repo, through "**Layout > Load Style...**".

#### Compiling

To compile the book and generate the PDF, just run this in a terminal:

```sh
. solfeo
```

This file contains the commands you need to type in order to compile the project:

```sh
rm -rf out
lilypond-book --output=out --pdf file-with-music-notation.lytex
cp solfeo.tex out
cd out && xelatex solfeo.tex && cd ..
mv out/solfeo.pdf .
evince solfeo.pdf &
```

Or if you prefer, you can type each command manually.

The first command tells LilyPond to generate a PDF output file. Since LilyPond will generate a lot of garbage files, use `--output=out` to tell it to generate a directory called `out` and store the output files there. Then, `xelatex` must be run against the `.tex` files generated by `lilypond-book` inside the `out` folder. The PDF should be generated in the root directory so that you can add the `out` directory to your `.gitignore` file. Finally, open the PDF with your favorite PDF viewer.

With this approach, garbage is kept isolated and gitignored, the workflow is easy to automate, and we get consistent trimming and LaTeX control of the typesetting.

**Notes:**
* If you have several `.lytex` files, you must compile each with `lilypond-book` (in a different line).
* If your document has a table of contents, list of figures, etc. you will have to run `xelatex` at least three times. This is normal in TeX documents, and is not related to LilyPond.

#### Folder structure

The scores are saved in the `scores` folder, and the output files generated by LilyPond are saved in the `out` folder. The `.lytex` files are saved in the root folder. LilyPond will generate `.tex` files inside the `out` folder, don't edit those because they will be overwritten everytime you compile.

## Dedicated blog

link (WiP)

## Licenses

[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org)
All code is [MIT licensed](http://opensource.org/licenses/MIT).

[![License](https://img.shields.io/badge/CC-BY_NC_4-green.svg?style=flat)](http://creativecommons.org/licenses/by-nc/4.0/legalcode)
The book is licensed [CC BY-NC 4.0](http://creativecommons.org/licenses/by-nc/4.0/legalcode).
