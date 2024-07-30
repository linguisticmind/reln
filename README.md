# reln

`reln` _(pronounced ree-L-N)_ allows the user to copy symlinks to a specified location, and adjust their targets such that they still point to the same files as the original links. The original links may then be removed. This allows the symlinks to be moved and copied in effectively the same way as one would do with the `mv` and `cp` commands when moving and copying regular files and directories, without needing to worry about adjusting the targets of the links according to their new location.

`reln` also provides options for converting relative target paths to absolute ones, and vice versa. Entirely new symlinks can also be created with `reln` by passing regular files or directories instead of links as positional arguments.

Also see a related tool [`unln`](https://github.com/linguisticmind/unln) for removing symlinks and their targets.

Video tutorial:

[![Mindful Technology - reln, unln: move symlinks fixing paths to targets, delete symlinks *and* their targets, and more](https://img.youtube.com/vi/jAlPWsBIhMM/0.jpg)](https://www.youtube.com/watch?v=jAlPWsBIhMM)

<a href='https://ko-fi.com/linguisticmind'><img src='https://github.com/linguisticmind/linguisticmind/raw/master/res/kofi/kofi_donate_1.svg' alt='Support me on Ko-fi' height='48'></a>

## Changelog

<table>
    <tr>
        <th>Version</th>
        <th>Date</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>
            <a href="https://github.com/linguisticmind/reln/releases/tag/v0.1.3">0.1.3</a>
        </td>
        <td>
            2024-07-05
        </td>
        <td>
            <p>
                Fixed incorrect handling of the target argument when only two non-option arguments are passed, and the target argument is a path to a symbolic link that points to a directory. Trailing forward slash can now be used to treat such a symbolic link as a directory; otherwise, it is treated as a regular file. Without a trailing forward slash, the symbolic link will be overwritten, or <code>reln</code> will throw an error&#8203;&mdash;depending on the <code>-y, --overwrite / -Y, --no-overwrite</code> setting; if a trailing forward slash is added, a new symbolic link will be put into the directory that the symbolic link passed as the target argument to <code>reln</code> is pointing to.
            </p>
        </td>
    </tr>
</table>

[Read more](CHANGELOG.md)

## Dependencies

`reln` was written and tested on Debian 12, and takes advantage of standard utilities that come with the system. In order to run `reln` on other systems, make sure that the following are installed and available on system's `PATH`:

* Bash >= 5.2.15
* Enhanced getopt
* GNU coreutils
* GNU sed

## Installation

1. Clone this repository to a directory of your choice (e.g. `~/repos`):

    ```bash
    cd ~/repos
    git clone https://github.com/linguisticmind/reln.git
    ```

2. Symlink or copy the [script file](reln) to a directory on your `PATH` (e.g. `~/bin`):

    ```bash
    cd ~/bin
    # To symlink:
    ln -sv ../repos/reln/reln
    # To copy:
    cp -av ../repos/reln/reln .
    ```

3. (OPTIONAL) Symlink or copy the [man page](man/man1/reln.1) to a directory on your `MANPATH` (e.g. `~/man`):

    ```bash
    cd ~/man/man1 # The `man` directory should contain subdirectories for different manual sections: `man1`, `man2` etc.
    # To symlink:
    ln -sv ../../repos/reln/man/man1/reln.1
    # To copy:
    cp -av ../../repos/reln/man/man1/reln.1 .
    ```

    A copy of the manual page is also [included in this README file](#manual).

4. (OPTIONAL) Copy the [example config file](config.bash) to the config directory:

    ```bash
    mkdir -v ~/.config/reln
    cp -v ~/repos/reln/config.bash ~/.config/reln
    ```

## Manual

```plain
RELN(1)                     General Commands Manual                    RELN(1)

NAME
       reln - recreate symlinks adjusting paths to their targets

SYNOPSIS
        reln [<options>] <link|file> <dir|link>[/]

        reln [<options>] <link|file> ... <dir>

DESCRIPTION
       reln  allows the user to copy symlinks to a specified location, and ad‐
       just their targets such that they still point to the same files as  the
       original links. The original links may then be removed. This allows the
       symlinks to be moved and copied in effectively  the  same  way  as  one
       would  do  with  the mv and cp commands when moving and copying regular
       files and directories, without needing to  worry  about  adjusting  the
       targets or the links according to their new location.

       reln  also provides options for converting relative target paths to ab‐
       solute ones, and vice versa. Entirely new symlinks can also be  created
       with  reln  by passing regular files or directories instead of links as
       non-option arguments.

       reln takes one or more links or non-link files as non-option  arguments
       (<link|file>),  while  the  last  non-option argument following all the
       <link|file>s is the destination (<dir>, <dir|link>), i.e. the  location
       for the new link(s).

       If  two or more <link|file>s are passed, then the destination must be a
       directory (<dir>). If only one <link|file> is passed, then  the  second
       and  last non-option argument may also point to a new name for the link
       to be created (<dir|link>), in which case the provided path may include
       a  path  to a destination directory as well as the filename for the new
       link. In either case, the destination directory must exist.

       In the case where only one <link|file> is passed,  a  trailing  forward
       slash  on  the  second and last non-option argument (<dir|link>) forces
       that argument to be treated as a directory (<dir>) rather than  a  link
       name  (<link>).  It is especially significant if the file passed as the
       second argument is a symbolic link pointing to a directory.  Without  a
       trailing  forward slash, the symbolic link will be overwritten, or reln
       will throw an error - depending on the state of -y, --overwrite  /  -Y,
       --no-overwrite;  if  a  trailing forward slash is added, a new symbolic
       link will be put into the directory that the symbolic  link  passed  as
       the second non-option argument is pointing to.

OPTIONS
   Passing arguments to options
       Enhanced  getopt  syntax applies when passing options. There is one im‐
       portant point to highlight when it comes to passing  options  with  re‐
       quired vs optional arguments.

       In  case  of  a short option, if an option takes a *required* argument,
       the argument may be written as a separate parameter, *or* directly  af‐
       ter  the  option  character. If an option takes an *optional* argument,
       however, the argument *must* be written directly after the option char‐
       acter.

       In case of a long option, if an option takes a *required* argument, the
       argument may be written as a separate parameter,  *or*  directly  after
       the  option name, separated by an equals sign (`=`). If an option takes
       an *optional* argument, however, the argument *must*  be  writtent  di‐
       rectly after the option name, separated by an equals sign (`=`).

                           Short option   Long option
       Required argument   -o <value>     --option <value>
                           -o<value>      --option=<value>
       Optional argument   -o[<value>]    --option[=<value>]

       Options  that  take optional arguments can be recognized in the options
       list below by their <value> and the preceding  equals  sign  being  en‐
       closed in square brackets:

       -o, --option[=<value>]

   General
       -r, --run
              Perform the specified operations instead of simulating them.

       -R, --no-run
              Simulate  the  specified  operations instead of performing them.
              This is the default.

       -p, --print-cmd
              Print a preview of the commands to be executed.

       -P, --no-print-cmd
              Do not print a preview of the commands to be executed.  This  is
              the default.

       -k, --keep-original
              Keep original symlinks.

       -K, --no-keep-original
              Do not keep original symlinks. Delete them. This is the default.

       -y, --overwrite
              Overwrite already existing files.

       -Y, --no-overwrite
              Do not overwrite already existing files. This is the default.

       -m, --mode={link|relink}
              Mode of operation.

              link   Create  links  to  specified  <link|file>s  regardless of
                     whether they are links or non-link files.

              relink (default)
                     Relink <link|file>s if they are links, and  create  links
                     to them if they are non-link files.

       -l, --link-type={relative|absolute|auto}
              Type of links to create.

              relative
                     Create relative links.

              absolute
                     Create absolute links.

              auto (default)
                     If  <link|file> is a link, create a link of the type cor‐
                     responding to the type  of  the  original  link's  target
                     path. If <link|file> is a non-link file, create a link of
                     the type that is  determined  by  --link-type-auto-files-
                     method.

       --link-type-auto-files-method={fallback|auto}
              Method  for  creating  links when -l, --link-type is `auto`, and
              <link|file> is a non-link file.

              fallback
                     Create a link of the type determined by --link-type-auto-
                     files-fallback.

              auto   Create  a  link of the type corresponding to type of path
                     to <file> passed to reln.

       --link-type-auto-files-fallback={relative|absolute}
              Type of link to  <file>  when  --link-type-auto-files-method  is
              `fallback`. The default value is `relative`.

       -L, --dereference-targets[={<integer>|inf}]
              Dereference link targets to a specified level. The default value
              is `0`.

              The value can be an integer greater than or equal to  0,  `inf`,
              or no value. Omitting the value is equivalent to passing `inf`.

   Other
       -c, --color
              Colorize the output. This is the default.

       -C, --no-color
              Disable colorization of the output.

       -h, --help
              Print help.

       -V, --version
              Print version information.

EXIT STATUS
       0   Success. No errors have occured.
       1   A general error has occured.
       2   Some links could not be created.

FILES
       A configuration file can be used to set default options.

       The configuration file's location is $XDG_CONFIG_HOME/reln/config.bash.
       If XDG_CONFIG_HOME is not set, it defaults to ~/.config.

AUTHOR
       Alex Rogers <https://github.com/linguisticmind>

HOMEPAGE
       <https://github.com/linguisticmind/reln>

COPYRIGHT
       Copyright © 2024 Alex Rogers. License GPLv3+:  GNU  GPL  version  3  or
       later <https://gnu.org/licenses/gpl.html>.

       This  is  free  software:  you  are free to change and redistribute it.
       There is NO WARRANTY, to the extent permitted by law.

RELN 0.1.3                           2024                              RELN(1)
```

## License

[GNU General Public License v3.0](LICENSE)
