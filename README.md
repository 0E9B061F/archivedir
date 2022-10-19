Archive files in a target directory older than a given age. Archived files are
placed in a subdirectory.

Installs two commands, `archivedir` and `archivedir_runner`. `archivedir` may be
run by hand and archives its target according to the options given.
`archivedir_runner` reads from `/etc/archivedirtab` and `/etc/archivedirtab.d/`
and calls `archivedir` once for each configuration found there. Each line of
these configruation files is expected to be a set of options and arguments to
`archivedir`, as they would be given on the command line.

A systemd service and timer are also included to run archive operations
automatically. Run `systemctl start archivedir.timer` to start the timer.

An example `archivedirtab`:

```
-t 30 -m -f -w /home/nn/camera
-t 90 -x -w /home/nn/notes
-t 30 -m -f -w /home/nn/screenshots
```

# USAGE

`archivedir [OPTIONS] TARGET`

Where `TARGET` is a directory to be archived.

* `-t DAYS`
  Archive limit in days. Files not modified within this period will be
  archived.  Default: 182
* `-z DEPTH`
  Maximum deth to descend to when considering files to archive. Default: 1
* `-x`
  Enable sticky files. Files with the sticky extension will never be
  archived. By default this is `x`.
  For example, `foo.x`, `bar.x.note`, and `baz.test.x.md` will all be
  considered sticky.
* `-X EXTENSION`
  Specify the extension used to mark files as sticky.
  Default: "x"
* `-m`
  Include month in dated archive name.
* `-d`
  Include day in dated archive name. Implies `-m`
* `-f`
  Flat mode. Rather than nesting dated archive structures, encode all date
  information in a single directory.
  For example, `TARGET/2022/10/19` becomes`TARGET/2022-10-19`
* `-w`
  Wrap mode. Places dated archive directory structures beneath a single
  archive root named "archive".
  For example, `TARGET/2022/10/19` becomes`TARGET/archive/2022/10/19`
* `-s`
  Simple mode. Archive files under `TARGET/archive` with no dated directory
  structure. Invalidates date-related options.
* `-h`
  Display a help message and exit.

Usage via `archivedir_runner` and its configuration files is recommended, rather
than running `archivedir` by hand. Using inconsistent options for the same
directory can create a difficult-to-fix mess. A consistent configuration
prevents this.
