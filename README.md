*(This tool is no longer in active development)*

Web Accessibility Toolbar
=========================

This repo contains the [Web Accessibility Toolbar
(WAT)](http://www.paciellogroup.com/resources/wat) including an [Inno
Setup](http://www.jrsoftware.org/isinfo.php) file for creating a
"setup.exe"-style installer.

There's [reference documentation](documentation.md) that explains what
you can do with the toolbar and includes keyboard shortcuts.

Currently this repo does not contain the source for the toolbar DLL, but
this is only the "shell" for the code; you can change virtually anything
by editing the scripts and then building the setup program with Inno
Setup.

Editable Files
--------------

These are the files that you can edit to modify the WAT.

### Accessibility\_Toolbar.xml

This is an xml file which creates the menu's and menu items in the WAT
UI. You can add/remove/modify the UI via this file. The text labels for
the UI controls are provided via variable (res\_id) references to the
Translation.ini

**For example:** The WAT \> Structure \> headings feature is represented
as this in the XML file:

``` {.xml}
<item resid="head1_struc" image="-1" />
```

### Translation.ini

Contains all the text strings provided in the UI and the functions. Also
includes mappings to invoke the scripts and inbuilt features via the UI.

### Scripts directory

The majority of the WAT functionality is powered by JS or WS files. (WS
just being a windows scripting host version -- but written in JS). You
can think of the features as bookmarklets, as this is how most of them
started life. You can modify an exsiting feature by changing its
corresponding script file.

**For example:** The WAT \> Structure \> headings is powered by
Headings.js, so you hack on that script to change the behaviour of the
feature.

### Icons directory

Icons can be added to menus/menu buttons/menu items.

**For example:** The Structure menu button (from the XML file
Accessibility\_Toolbar.xml)

``` {.xml}
<button type="button" resid="Structure" accesskey="6" image="structure.bmp">
```

Building
--------

You must have [Inno Setup](http://www.jrsoftware.org/isinfo.php)
installed to build a `setup.exe`-style installer.

You can build an installer for 32-bit machines, or one for 64-bit
machines (which also includes the 32-bit binaries, so you can use IE in
32- or 64-bit mode). There are two ways to do this.

-   **Easy:** Double-click on `build32.bat` or `build64.bat`. This will
    open a command prompt window in which the installer build progress
    will be displayed. When the build is complete, you can press any key
    to close the window.

    Note for network folder users: Windows doesn't get on well with
    launching batch files from network folders (as cmd.exe doesn't
    support UNC paths), so you can either explore the folder via a
    mapped drive, or [open a command prompt window in the network
    folder](http://stackoverflow.com/a/379804) and type the name of the
    batch file.

-   **1337:** Open `Web-Accessibility-Toolbar.iss`; the comments in the
    file explain how to make a build (you only need to change one line
    of the file).

Development Info
----------------

Please use tabs for indentation (we recommend a tabstop of four).

Before committing, please remember to build and test, and consider
incrementing the version number (it's in `wat/Translation.ini` under the
"Version" key and currently it is the release date, but it needn't be).

The file `wat/Translation.ini` is in UTF-16, which Git can't cope with.
However, you can use an external diff tool, such as vimdiff (or mvimdiff
if you have MacVim).

-   To use vimdiff:

        git config --global diff.tool vimdiff

-   To use mvimdiff takes a little extra work:

        git config --global diff.tool gvimdiff
        git config --global difftool.gvimdiff.path `which mvimdiff`

The use of `--global` changes the setting in your home directory, rather
than just the current repository; if you only want to change this
setting for the WAT repository, drop the `--global` part.

> This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.
