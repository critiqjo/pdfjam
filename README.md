#pdfjam

**NOTE**: `pdfjam` is probably distributed along with the `texlive` package of your Linux distribution. This repo is just a mirror for my own convinience. This markdown file was generated from the original html file using the amazing converter by domchristie, [to-markdown](https://github.com/domchristie/to-markdown).

_Author_: David Firth, [http://go.warwick.ac.uk/dfirth](http://go.warwick.ac.uk/dfirth)

**This file is kept up to date at [http://go.warwick.ac.uk/pdfjam](http://go.warwick.ac.uk/pdfjam).**

*   [Overview](#overview)
*   [Pre-requisites](#prereq)
*   [Documentation](#documentation)
*   [Download](#download)
*   [Installation/configuration](#install)
*   [Using the scripts](#using)
*   [Mac OS X only: drag-and-drop](#droplets)
*   [FAQ](#faq)
*   [Reporting bugs](#bugs)
*   [Version history](#history)

<a name="overview"></a>

## Overview

**PDFjam** is a small collection of shell scripts which provide a simple interface to much of the functionality of the excellent [pdfpages ![PDF file](http://www2.warwick.ac.uk/brands/icons/acrobat.gif "PDF file")](http://www.ctan.org/tex-archive/macros/latex/contrib/pdfpages/pdfpages.pdf "Link to the pdfpages manual (PDF)") package (by Andreas Matthias) for [pdfLaTeX](http://www.tug.org/applications/pdftex/). These scripts take one or more PDF files (and/or JPG/PNG graphics files) as input, and produce one or more PDF files as output. They are useful for joining files together, selecting pages, reducing several source pages onto one output page, etc., etc.

The main script is named **`pdfjam`**. This is the core of the package.

All of the other scripts provided in the PDFjam package are optional extras. They are simple wrappers for calls to `pdfjam`, designed to perform some common tasks such as joining or n-upping PDF files or to illustrate other features; they are not very elaborate, nor are they extensively tested. They are probably best thought of as simple templates that can be used for constructing more elaborate wrapper scripts as required. At present the wrapper scripts distributed in the PDFjam package are:

*   **`pdfnup`**, which allows one or more PDF files to be "n-upped" in roughly the way that [`psnup`](http://www.tardis.ed.ac.uk/~ajcd/psutils/psnup.html) does for PostScript files. (This was the original motivation: for files that have to be printed, or have to be made available to dozens or hundreds of other people for printing, n-up formatting saves trees!)
*   **`pdfpun`**, similar to `pdfnup` but arranges the source pages right-to-left on the output page, ie in a format more suitable for right-to-left languages. This script works only on one file at a time. (Thanks to Ido for suggesting this.)
*   **`pdfjoin`**, which combines the pages of multiple PDF files together into a single file.
*   **`pdf90`**, **`pdf180`** and **`pdf270`** which rotate the pages of one or more PDF files.
*   **`pdfflip`** which reflects the pages of one or more PDF files. (Suitable for making transparencies if you want to write on the back of them!)
*   **`pdfbook`** which arranges pages into 2-up "signatures" (like [`psbook`](http://www.tardis.ed.ac.uk/~ajcd/psutils/psbook.html) does for PostScript files), suitable for binding into a book. (Many people have suggested that this would be useful — I hope it is!)
*   **`pdfjam-pocketmod`** which converts 8 pages from a single PDF file into a pocket-sized booklet. ([Folding instructions here!](http://repocketmod.com/) Thanks to Thomas Nemeth for suggesting this.)
*   **`pdfjam-slides6up`** and **`pdfjam-slides3up`** which process PDF presentation slides to six-per-page or three-per-page for handout purposes.

A potential drawback of `pdfjam` and other scripts based upon it is that any hyperlinks in the source PDF are lost. On the positive side, there is no appreciable degradation of image quality in processing PDF files with these programs, unlike some other indirect methods such as  `pdf2ps | psnup | ps2pdf`  (in the author's experience).

These tools are designed for Unix-like systems, including Linux and Mac OS X. It seems that they will work also on Windows computers with a suitable installation of [Cygwin](http://www.cygwin.com/) (with the Cygwin `tetex-extras` package installed), but this has not been extensively tested.

An alternative set of PDF manipulation tools, which are java-based, is provided by the [Multivalent](http://multivalent.sourceforge.net/) project. They do much the same things as `pdfjam`, and quite a bit more. Hyperlinks don't seem to be preserved there either, though, when n-upping a document.

For Mac OS X, n-up with a more visual interface is provided by [PDF Nup Maker](http://evolve.lse.ac.uk/software/PDFNupMaker/). Like `pdfjam`, this is a front end to pdflatex/pdfpages.

The PDFjam software is made available free, under GPL version 2 (see the file named `COPYING` that is included with the package). It comes with ABSOLUTELY NO WARRANTY of fitness for any purpose whatever.

<a name="prereq"></a>

## Pre-requisites

1.  A Unix-like operating system (Linux, Mac OS X, Solaris, etc.; possibly Cygwin)
2.  A working, up-to-date installation of [pdfTeX](http://www.tug.org/applications/pdftex) (including `pdflatex` and an up-to-date copy of [`pdftex.def`](http://pdftex-def.berlios.de/))
3.  A working installation of the LaTeX package [pdfpages](http://www.ctan.org/tex-archive/macros/latex/contrib/pdfpages) (version 0.4f or later)

Some of the options offered by `pdfjam` also require the LaTeX packages [geometry](http://www.ctan.org/tex-archive/macros/latex/contrib/geometry/) and [hyperref](http://www.ctan.org/tex-archive/macros/latex/contrib/hyperref/).

<a name="documentation"></a>

## Documentation

The primary documentation for `pdfjam`, and hence for the other scripts that call it, is obtained by

```sh
pdfjam --help
```

This gives information on the arguments to `pdfjam`, and the default settings that apply at your installation. In addition to the arguments that are explicitly documented there, `pdfjam` provides access to all of the options of the pdfpages package: that's a large number of options, and it's a set of options that might change, so users are referred to the current [pdfpages manual ![PDF file](http://www2.warwick.ac.uk/brands/icons/acrobat.gif "PDF file")](http://www.ctan.org/tex-archive/macros/latex/contrib/pdfpages/pdfpages.pdf "Link to the pdfpages manual (PDF)") to see what's available.

In addition, each of the scripts has a (rather basic) `man` page. For example,

```sh
man pdfjam-pocketmod
```

gives information about usage and other aspects of the `pdfjam-pocketmod` script.

<a name="download"></a>

## Download

PDFjam is a project at [freshmeat](http://freshmeat.net/projects/pdfjam/): please subscribe there to receive update announcements.

Download the shell scripts as [pdfjam\_latest.tgz](http://www2.warwick.ac.uk/fac/sci/statistics/staff/academic/firth/software/pdfjam/pdfjam_latest.tgz).

(If for some reason you don't want the latest version, you can still get older versions. Since version 2.00 the URLs are all of the form `http://go.warwick.ac.uk/pdfjam/pdfjam_VN.tgz`, with "VN" representing the version number. So "VN" could be 2.00, 2.01, 2.02, 2.03 or 2.04; from PDFjam version 2.05 onwards, the dot will be omitted from the version number in the file name, so "VN" will be 205, 206, etc.)

Various people have kindly packaged PDFjam for distribution in other ways (and perhaps there are some not listed here?):

*   Eduard Bloch has packaged [PDFjam for Debian](http://packages.debian.org/unstable/text/pdfjam)
*   Paul Chvostek has made a [port to FreeBSD](http://www.freebsd.org/cgi/ports.cgi?query=pdfjam)
*   Pander has provided a link to [Ubuntu packages](http://packages.ubuntu.com/search?keywords=pdfjam)
*   Petr Uzel has made available [openSUSE packages](http://software.opensuse.org/search?baseproject=ALL&p=1&q=pdfjam)
*   Alexis Ballier has provided a [Gentoo package](http://packages.gentoo.org/package/app-text/pdfjam)
*   Karl Berry has provided a [CTAN package](http://mirror.ctan.org/support/pdfjam).

Cosmin Popescu has written a [front-end to the pdfnup script, based on Qt](http://qt-apps.org/content/show.php/pdfnup-gui?content=134874.).

To download some stand-alone _Mac OS X droplets_ (based on PDFjam version 1.21), see [below](#droplets).

<a name="install"></a>

## Installation/configuration

The shell scripts in the _bin_ sub-directory of the package should be placed on the PATH of anyone who needs to use them.

The man files in the _man1_ sub-directory should be installed on the `MANPATH` of all who need to read them.

On many unix-like systems the scripts should run without any further configuration, provided that the pre-requisite TeX installation is present. If you want to check (e.g., prior to installation) that `pdfjam` will work on your system, please unzip the _tests_ sub-directory of the package and follow the instructions that appear in `tests/README-tests.txt`.

If configuration _is_ needed, this can be done through a site-wide or user-specific configuration file. This might be necessary if, for example, your site has a non-standard TeX installation, or a non-standard location for temporary files, or a paper size that is different from the A4 international standard.

The file [`pdfjam.conf`](pdfjam.conf "Sample pdfjam configuration file, plain text") is a sample configuration file which can be edited as needed. After editing, either install the file for site-wide use (at `/etc/pdfjam.conf`, `/usr/share/etc/pdfjam.conf`, `/usr/local/share/pdfjam.conf`, or `/usr/local/etc/pdfjam.conf`) or as a user-defaults file at `~/.pdfjam.conf`. User settings made at `~/.pdfjam.conf` override corresponding settings made in a site-wide configuration file.

For example, if you want your own output to be on "US letter" size paper by default, simply put the line

```sh
paper=letterpaper
```

in a plain text file named file `.pdfnup.conf` in your home directory. (The code word `letterpaper` is how LaTeX refers to that particular page size; for other available paper sizes, please see the output of `pdfjam --help`.)

On some systems it might even be necessary to change the list of places (i.e., `/etc/pdfjam.conf` and others as listed above) that is searched for site-wide configuration files. This can only be done by editing the `pdfjam` script itself. To see which directories on _your_ system are searched for a file named `pdfjam.conf`, use

```sh
pdfjam --configpath
```

<a name="using"></a>

## Using the scripts

For a full overview of what `pdfjam` can do, the importance of the [pdfpages manual ![PDF file](http://www2.warwick.ac.uk/brands/icons/acrobat.gif "PDF file")](http://www.ctan.org/tex-archive/macros/latex/contrib/pdfpages/pdfpages.pdf "Link to the pdfpages manual (PDF)") cannot be stressed enough! The following examples merely serve as a brief introduction.

### Example 1

Consider converting each of two documents to a side-by-side "2-up" format. Since we want the two documents to be processed separately, we'll use the `--batch` option:

```sh
pdfjam --batch --nup 2x1 --suffix 2up --landscape --outfile . file1.pdf file2.pdf
```

This will produce new files `file1-2up.pdf` and `file2-2up.pdf` in the current working directory. The above call could be shortened a bit, by using `pdfnup`, to

```sh
pdfnup --batch --suffix 2up file1.pdf file2.pdf
```

In a 'vanilla' installation of `pdfjam`, the default for `--outfile` is the current working directory.

### Example 2

Suppose we want a single new document which puts together selected pages from two different files:

```sh
pdfjam file1.pdf '{},2-' file2.pdf '10,3-6' --outfile ../myNewFile.pdf
```

The new file `myNewFile.pdf`, in the parent directory of the current one, contains an empty page, followed by all pages of `file1.pdf` except the first, followed by pages 10, 3, 4, 5 and 6 from `file2.pdf`.

The resulting PDF page size will be whatever is the default paper size for you at your site. If instead you want to preserve the page size of (the first included page from) `file1.pdf`, use the option `--fitpaper true`: this is the default action of the `pdfjoin` convenience script.

(All pages in an output file from `pdfjam` will have the same size and orientation: for joining together PDF files while preserving different page sizes and orientations, `pdfjam` is not the tool to use; and since `pdfjoin` simply calls `pdfjam`, the same comment applies also to `pdfjoin`. I'm told that if you have [Ghostscript](http://pages.cs.wisc.edu/~ghost/) installed, something along these lines might more nicely join files with different page sizes and orientations:

```sh
gs -dBATCH -dNOPAUSE -q -sDEVICE=pdfwrite -sOutputFile=finished.pdf file1.pdf file2.pdf
```

But I haven't tried it.)

### Example 3

To make a portrait-oriented 4-up file from the pages of three input files, with a thin-line frame around the input pages,

```sh
pdfjam file1.pdf file2.pdf file3.pdf --no-landscape --frame true --nup 2x2 \
         --suffix 4up --outfile ~/Documents
```

Here a _directory_ was specified at `--outfile`: the resultant file in this case will be ~/Documents/file3-4up.pdf. (Note that **if there's a writeable file with that name already, it will be overwritten**: no check is made, and no warning given.)

### Example 4

Suppose we have a document made up of "US letter" size pages, and we want to convert it to A4:

```sh
pdfjam 'my US letter file.pdf' --a4paper --outfile 'my A4 file.pdf'
```

### Example 5

A useful application of `pdfjam` is for producing a handout from a file of presentation slides. For slides made with the standard 4:3 aspect ratio a nice 6-up handout on A4 paper can be made by

```sh
pdfjam --nup 2x3 --frame true --noautoscale false --delta "0.2cm 0.3cm" \
         --scale 0.95 myslides.pdf --outfile myhandout.pdf
```

The `--delta` option here comes from the pdfpages package; the `--scale` option is passed to LaTeX's `\includegraphics` command.

The two wrapper scripts `pdfjam-slides6up` and `pdfjam-slides3up` are provided in order to make this particular application of `pdfjam` easy: for example,

```sh
pdfjam-slides3up --pagenumbering true --batch slides1.pdf slides2.pdf
```

makes a pair of 3-up handouts `slides1-3up.pdf` and `slides2-3up.pdf`, with space for side-notes and with the handout pages numbered.

(Slides made by LaTeX's _beamer_ package, using the `handout` class option, work especially nicely with this!)

### Example 6

Suppose we want to trim the pages of our input file prior to n-upping. This can be done by using a pipe:

```sh
pdfjam myfile.pdf --trim '1cm 2cm 1cm 2cm' --clip true --outfile /dev/stdout | \
  pdfnup --frame true --outfile myoutput.pdf
```

The `--trim` option specifies an amount to trim from the left, bottom, right and top sides respectively; to work as intended here it needs also `--clip true`. These (i.e., `trim` and `clip`) are in fact options to LaTeX's `\includegraphics` command (in the standard _graphics_ package).

(Thanks to Christophe Lange and Christian Lohmaier for suggesting an example on this.)

### Example 7

To offset the content of double-sided printed pages so that they are suitable for binding with a [Heftstreifen](http://de.wikipedia.org/wiki/Heftstreifen), use the `--twoside` option:

```sh
 pdfjam --twoside myfile.pdf --offset '1cm 0cm' --suffix 'offset'
```

### Example 8

To use PDF input files whose names do not end in "`.pdf`", you will need to use the `--checkfiles` option. This depends on the availability of the `file` utility, with support for the options `-Lb`; this can be checked by trying

```sh
file -Lb 'my PDF file'
```

where `'my PDF file'` is the name of a PDF file on your system. The result should be something like "`PDF document, version 1.4`" (possibly with a different version number).

With "`file -Lb`" available, we can use PDF files whose names lack the usual "`.pdf`" extension. For example,

```sh
pdfnup --checkfiles 'my PDF file'
```

should result in a file named "`my PDF file-nup.pdf`" in the current working directory.

### Example 9

If you want to print a landscape-oriented PDF document on both sides of the paper, using a duplex printer that does not have 'tumble' capability, make a new version with every second page rotated for printing:

```sh
pdfjam --landscape --doublepagestwistodd true my-landscape-document.pdf
```

### Example 10

Please feel free to suggest other examples that might help people! (For the email address, see [reporting bugs](#bugs))

<a name="droplets"></a>

## Mac OS X only: drag-and-drop

Under **Mac OS X**, [DropScript](http://www.wsanchez.net/software/) has been used to make some simple drag-and-drop applications. Some sample droplets are provided in [pdfdroplets_1.21.dmg](http://www.warwick.ac.uk/go/pdfjam/pdfdroplets_1.21.dmg): these may be all you'll need! The sample droplets look like this:

<center>![](pdfdroplets.png)</center>

These droplets assume that your pdflatex is at `/usr/texbin/pdflatex`. If pdflatex lives somewhere else on your system, the droplets won't work until you include in your home directory a file named `.pdfnup.conf` (or there is a system-wide file `pdfnup.conf` at one of the four locations listed above), containing the line

```sh
pdflatex=/path/to/pdflatex
```

where `/path/to/pdflatex` is the answer you get when you type `which pdflatex` in the Terminal. (If you get no answer, chances are that you do not have `pdflatex` installed on your Mac; if you need to install it, you could just download and install [MacTeX](http://www.tug.org/mactex) or one of its slimmed-down variants.)

<a name="faq"></a>

## FAQ

**1\. Why "PDFjam"?**
Because it's for PDF files, and jam is what I like best on my toast (well, second best after marmalade, anyway).

**2\. The thing runs but the output doesn't look the way it should. Why?**
Most likely either your pdfTeX or your pdfpages installation is an old version. (Check also that `pdftex.def`, to be found in in `.../texmf/tex/latex/graphics/`, is up to date.) If the problem persists even with up-to-date versions of pdfTeX, `pdftex.def` and pdfpages, then please do report it.

<a name="bugs"></a>

## Reporting bugs

Please report any bugs found in these scripts, to d.firth (at warwick.ac.uk).

### Some known problems:

*   In _Cygwin_, using `pdfjam` in a pipeline does not seem to work. Scripts like `pdfjam-pocketmod`, which use pipelines, therefore do not work there. The problem seems to be with _Cygwin_'s handling of file descriptors within pipelines.

Solving these problems is on the to-do list: if you have solved one of them already please let me know!

<a name="history"></a>

## Version history

**2.08**: fixed a bug in one of the tests [2010-11-14]

**2.07**: two other common graphics formats (JPG and PNG) are now explicitly allowed as input files (i.e., not only PDF files are allowed as inputs). [2010-11-13]

**2.06**: changed the `pdfbook` script to include `--booklet true` as the default behaviour (thanks to Julien Bossert for this good suggestion). [2010-05-11]

**2.05**: changes to the `pdfbook` script [the `--right-edge-binding` option is now redundant, and there's a new `--short-edge` option for binding along the short edge of pages instead of the long edge (thanks to Marco Pessotto for this)]. The `--preamble` option to `pdfjam` is enhanced, to allow multiple instances which get concatenated. Also various minor corrections to man pages. [2010-04-25]

**2.04**: various minor improvements suggested by Debian maintainers (thanks to Eduard Bloch for these). The main things are: addition of the `--version` option; liberalisation of `pdfjam` to allow files in _JPEG_ format to be specified as input, as well as PDF (I don't know why or if this might work! but some people have said it does); tidying of the man files; and more use of `exec`, to avoid forking. [2010-04-22]

**2.03**: fixed a bug which caused problems when your `/bin/sh` is the _zsh_ shell; fixed a bug which prevented the correct representation of many UTF-8 characters in `pdfinfo` data. [2010-04-20]

**2.02**: more progress on portability; introduced the beginnings of a suite of tests; improvements in the `--keepinfo` functionality, and in the treatment of file permissions (thanks to Marco Pessotto for these). [2010-04-14]

**2.01**: fixed a silly bug (thoughtless use of "`test -a`" in a couple of places) which seriously affected portability. [2010-04-13]

* * *

**2.00**: a **major re-design**. This is not completely backward-compatible with previous versions of the `pdfnup`, `pdfjoin` and `pdf90` scripts. The differences in interface are few, though, and the main ones are listed below.

The main changes are:

*   The new script `pdfjam` now does all the work; all the other scripts included with the package are just simple wrappers for `pdfjam`.
*   `pdfjam` makes available essentially _all_ of the facilities of the pdfpages package (without having to know what they are).
*   Various security and portability issues have been resolved. (None of the scripts now calls for `/bin/bash`; and the handling of temporary files is now much safer.)
*   `pdfjam` can take PDF input from `/dev/stdin`, and send output to `/dev/stdout`. (This allows `pdfjam` to be used in a pipeline.)
*   If the `--outfile` option specifies a relative path, that path is now relative to the _current working directory_ (as is normally expected of unix utilities). **This is different behaviour from previous versions.**
*   With multiple input files, `pdfjam` offers two distinct methods of processing. The default is to take pages as specified from the input files, and combine them into a single document. If the `--batch` option is used, `pdfjam` operates _separately_ on the input files, producing one output file per input file. **This is different behaviour from previous versions.**
*   Page selection is available separately for each input file. A **difference from previous versions** is that the `--pages` keyword is no longer used.
*   `pdfjam` uses the `\includepdfmerge` command from _pdfpages_, as a result of which all pages in an output file have the same size and orientation. **This is different behaviour from previous versions.**
*   Output page orientation is now controlled by using `--landscape` (negated, if necessary, by `--no-landscape`). The previous `--orient` option is no longer used, and in particular "`--orient auto`" is no longer available. **This is different behaviour from previous versions.**
*   Other new features include:
    *   `--keepinfo` option, to allow preservation of PDF document information, if the `pdfinfo` utility and the LaTeX `hyperref` package are available (thanks to Robert Wenner for suggesting this);
    *   `--pdftitle`, `--pdfauthor`, `--pdfsubject` and `--pdfkeywords` options, to specify new PDF document information (these require the LaTeX `hyperref` package);
    *   many more "named" output page sizes are available if the LaTeX `geometry` package is installed (the full list of allowed paper specifications is: `a0paper, a1paper, a2paper, a3paper, a4paper, a5paper, a6paper b0paper, b1paper, b2paper, b3paper, b4paper, b5paper, b6paper letterpaper, executivepaper, legalpaper`;  thanks to Corné Verbruggen and Mel Irizarry for suggesting this) and non-standard page sizes can also be defined;
    *   `--checkfiles` option to request that input files be checked using the `file` utility, rather than requiring the file name to end in "`.pdf`" or "`.PDF`";
    *   `--twoside` option, to allow the LaTeX _twoside_ class option to be specified (thanks to Johannes Reinhard for suggesting this);
    *   `--pagecolor` option, to allow the background colour of output pages to be changed (thanks to James Fisher for suggesting this);
    *   `--vanilla` option to run `pdfjam` without reading site-wide or user configuration files.

In addition, various reported bugs have been fixed — many thanks to all those kind people who reported them (too numerous to list here!) [2010-03-14]

* * *

**1.21**: bug fixes, including security issues (many thanks to Eduard Bloch, Robert Buchholz and Martin Vaeth for helpful reports on vulnerabilities and for kindly contributing patches); the scripts now call for `/bin/bash` as interpreter; availability of `mktemp` is now also assumed; the Mac OS X droplets now look for `pdflatex` at (by default) `/usr/texbin/pdflatex` [2009-01-19]

**1.20**: added minimal man pages; added extra possible locations for the site-wide configuration file [2005-01-25]

**1.11**: added the `--scale` option to pdfnup, which allows page margins either to be enlarged (e.g,. `--scale 0.9`) or reduced (e.g,. `--scale 1.1`) by scaling the page contents. By popular request! [2004-10-13]

**1.10**: output files now appear by default in same directory as input, rather than in the current working directory; fixed a bug that caused the scripts not to work on some versions of Solaris (thanks to Daniel Gebhart); major improvements to the Mac OS X sample droplets. [2004-06-24]

**1.03**: minor changes towards POSIX compliance. [2004-05-09]

**1.02**: added a COPYING file to the package. [2004-05-08]

**1.00**: package re-named PDFjam. [2004-05-07]

**0.99a**: a minor change to the output of `pdfnup --help` and `pdfjoin --help` [2004-05-06]

**0.99**: various improvements to pdfnup, including the handling of multiple PDF input files. Added pdfjoin and pdf90\. [2004-05-05]

**0.97**: corrections to the output of `pdfnup --help` [2004-04-23]

**0.96**: minor changes to comments in the pdfnup script [2004-02-12]

**0.95**: added the possibility of site-specific and user-specific configuration files (thanks to Jason Lewis for suggesting this) [2004-01-28]

**0.9**: added `--openright` (thanks to Jason Lewis for suggesting this) [2004-01-28]

**0.8**: added `pdfnup --help` facility (thanks to Wilfrid Kendall for this suggestion) [2003-09-12]

**0.7**: paths involving spaces now permitted; page trimming added (thanks to Alex Montgomery for suggesting that); default output filename now has a dash inserted before the "nup" label (as in `wasteful-2x2.pdf` ); sample Mac OS X droplets provided [2003-01-26]

**0.6**: use of paths involving spaces now reports an error [2002-08-22]

**0.5**: fixed a bug which caused incompatibility with some types of unix [2002-06-24]

**0.4**: better error trapping, improved portability [2002-04-30]

**0.3**: first public release of pdfnup [2002-04-04]
