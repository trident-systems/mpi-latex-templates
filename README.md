MPI Latex Templates
=========================

This package generates LaTeX class and style files to create New Zealand  Ministry of Primary Industries (MPI) 
fisheries reports. The  style files can be built and installed manually, or can be installed using debian on
Linux systems.

## Installing the package

### Checking LaTeX
Before you can install the package you must check to make sure you
have the right version of LaTeX installed. To do this run the command:

        xelatex --version

Which should give the output

        XeTeX 3.1415926-2.4-0.9998 (TeX Live 2012/Debian)
        kpathsea version 6.1.0
        Copyright 2012 SIL International and Jonathan Kew.
        There is NO warranty.  Redistribution of this software is
        covered by the terms of both the XeTeX copyright and
        the Lesser GNU General Public License.
        For more information about these matters, see the file
        named COPYING and the XeTeX source.
        Primary author of XeTeX: Jonathan Kew.
        Compiled with ICU version 49.1 [with modifications for XeTeX]
        Compiled with zlib version 1.2.3.4; using 1.2.3.4
        Compiled with FreeType2 version 2.4.8; using 2.4.8
        Compiled with fontconfig version 2.8.0; using 2.8.0
        Compiled with libpng version 1.2.46; using 1.2.46
        Compiled with poppler version 0.18.4


If you have an older version of LaTeX you will need to install the backport for
LaTeX. 

### Checking for the fonts

In order to use the package you will need to have the following fonts installed:

 - Times New Roman
 - Arial

To check if the font is present run `fc-list` and see if the font name is present
in the output.

All of the font files must be places in an appropriate location 
where the fonts can be seen by the system. Two possible locations for Linux 
systems are `~/.fonts` and `/usr/local/share/fonts`.


### Installing the Package
To install the package run the following commands

          git clone git@github.com:dragonfly-science/mpi-latex-templates.git
          cd mpi-latex-templates
          make pkg
          sudo dpkg -i ../mpi-latex-templates_1.3ubuntu1_all.deb

#### Manual Installation

The package will only build on 64-bit linux machines. This is an unfortunate 
side effect that comes from the latex version installed on the machines at the
moment being a little bit too old. As a result the biber binary and biblatex package
are included in this repository. 

In the case of manual installation, the following steps are required. 


**Get the correct biber binary**

If you are not on a x64 linux machine you will need to replace the biber binary in
the repository with the correct one for your OS and architecture. Binaries can be found
at http://sourceforge.net/projects/biblatex-biber/files/biblatex-biber/1.8/binaries/.
Note that you must use version 1.8.

**Build the package** 

Run `make all`

**Identify where you can install latex files**

On Linux and OS X run the command: `kpsepath tex | tr ':' '\n'` which will give a list
of directories which latex will look for files in. 

**Install the mpi templates**

Create a directory called `mpi` in the latex tree and place all the `.sty`
and `.cls` files into it. Copy the biblatex-mpi into the same directory as the 
`mpi` directory. You should now have two new directories. A common 
location for these would be 

 * /usr/share/texlive/texmf-dist/tex/latex/mpi
 * /usr/share/texlive/texmf-dist/tex/latex/biblatex-mpi


**Install biblatex and biber**

On many systems this may not be necessary as the package may work using the 
system versions of biblatex and biber. If this is not the case then you will
need to find the biber binary on your system and replace it with the binary
that you downloaded earlier in `Get the correct biber binary`. You will also
need to find the `biblatex` directory in your latex system and replace it with
the biblatex directory included with this repository. The following command
will help you find the biblatex directory: `kpsewhich biblatex.sty`.


**Tell latex about the new package**

To ensure that LaTeX is aware of the new package you will need to run: `texhash`.

## Using the package

At this point the following latex classes will be available for you to use:

 - mpi-aebr
 - mpi-far

You will also have access to the `mpi` package.

## Documentation

Package is generated in the file `mpi.pdf`. There is an example tex file showing how it can be used. 

The example files are:

 - mpi-aebr.tex
 - mpi-far.tex


## Incompatible Packages

The mpi templates package will not work correctly with the following packages:

 - subfig (use subcaption instead)

