`ORG.FSMS:`
![GitHub release (latest by date)](https://img.shields.io/github/v/release/FS-make-simple/porg)
![GitHub Release Date](https://img.shields.io/github/release-date/FS-make-simple/porg)
![GitHub repo size](https://img.shields.io/github/repo-size/FS-make-simple/porg)
![GitHub all releases](https://img.shields.io/github/downloads/FS-make-simple/porg/total)
![GitHub](https://img.shields.io/github/license/FS-make-simple/porg)  

# p*org

## What's porg?

Porg (formerly known as paco), is a program to aid management of software
packages installed from source code.

After the installation of such packages, one is usually left with having no
idea of what it was installed and where it all went, making it difficult to
uninstall the package in the future. Porg was written to solve this problem in
a quite simple fashion.

When installing a package from sources, porg wraps the install command (e.g.
"make install"), and saves installation information into a text database.

The following sequence of commands exemplify a typical installation of a
package named foo-1.3:
```sh
    $ tar xvf foo-1.3.tar.gz
    $ cd foo-1.3
    $ ./configure
    $ make
    $ sudo porg -lp foo-1.3 "make install"
```
After the above commands, and provided that everything went fine, the program
foo-1.3 will be installed into the system, and registered into the porg
database. One can check it by simply typing the following command, which would
list the files installed by the package:
```sh
    $ porg -f foo-1.3
```
Porg also provides options for listing packages, sizes, file counts, removing
packages or printing package information.

## Changes from the last version of paco

    * Disabled the options for removing shared files when uninstalling a
      package, both in porg and grop. Now shared files are never removed, as it
      ougth to be.
    * Disabled listing of shared files.
    * Simplification of the GUI.
    * Simplification of the package database. No need to update it anymore.
    * Major code enhancements and cleanup.
    * Additionally, all changes documented in the Changelog.

Paco users can import old paco logs into the porg database with the script
paco2porg included in the porg distribution.

## Technichal details

To keep track of the files installed by the packages, porg loads a shared
library before installation by using the environment variable LD_PRELOAD (or
DYLD_INSERT_LIBRARIES in MacOS). During the installation, this library catches
the system calls that cause filesystem alterations (like open, link, rename,
...), and logs the created files into a text file.

Since the preloaded library is used only by the specific installation process,
the created logs are not contaminated with files created by any other process.
Thus porg can be used to track parallel installations.

Please note that porg does not work on systems in which the executables
involved in the installation of the packages (mv, cp, install...) are
statically linked against libc, like FreeBSD and OpenBSD.

## Grop

Grop is the graphic interface of porg. It uses and depends on the GTKMM library
(version 3.4.0 or later). It's not meant to be a replacement of porg, since it
lacks some important features like logging package installations, but it allows
for manipulating the installed packages in a more comfortable way.

Grop is installed by default, unless option "--disable-grop" is pased to
configure.

## Auxiliary scripts

The porg distribution provides the following auxiliary scripts:

    * paco2porg

      A shell script that imports paco logs into the porg database.

    * porgball

      A shell script that creates binary tarballs (or "porgballs") from
      packages that are logged in the porg database. It can be used also to
      reinstall packages by extracting the files from previously created
      porgballs.

    * porg_bash_completion

      This file, written by Christian Schneider, provides bash completion
      support for porg, in systems that have programmable bash completion
      enabled.

## License

Copyright © 2016 David Ricart.  
Porg is protected by the GNU General Public License.  
Look at the COPYING file for more details.  

## Authors

The creator and maintainer of porg is David Ricart <icnelis@*> (where * = gmail.com).

I'd like to thank all the males that have contributed to the development of
porg. A complete list of them can be found in the AUTHORS file.
