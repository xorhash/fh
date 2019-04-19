# fh: file history

**fh** records changes to a file on a per-file basis,
similar to [RCS](https://en.wikipedia.org/wiki/Revision_Control_System) and
[SCCS](https://en.wikipedia.org/wiki/Source_Code_Control_System).
It is, however, considerably more primitive.

Design goals:

- no support for multi-user environments (no locking, etc.)
- implemented in shell script
- must use ed(1)
- should work or easily be made to work on 7th Edition UNIX

I've taken care not to use any shell scripting constructions that didn't
exist in the Bourne shell, but I may have missed things;
however, the shebang needs to be removed on 7th Edition UNIX.

**fh** uses a chain of ed(1) scripts to construct any version of a file.
It even allows recording of commit messages.

## Why?

I saw the following passage in [diff(1) of 7th Edition UNIX](https://man.openbsd.org/UNIX-7/diff.1):

> The **-e** option produces a script of *a*, *c* and *d* commands for the editor *ed*, which will recreate *file2* from *file1*. The **-f** option produces a similar script, not useful with *ed*, in the opposite order. In connection with **-e**, the following shell program may help maintain multiple versions of a file. Only an ancestral file ($1) and a chain of version-to-version *ed* scripts ($2,$3,...) made by *diff* need be on hand. A `latest version' appears on the standard output.
>
>     (shift; cat $*; echo ´1,$p´) ⎪ ed - $1

After some thinking, I figured it would be hilarious to actually implement a basic version control system on these primitives.
In hindsight, it's probably closer to terrifying than hilarious.

## License

ISC, see LICENSE.

## Installation and usage

Copy the `fl`, `fr` and `fu` files to a directory in `$PATH`;
make sure they are marked as executable.
Copy the man pages `fl.1`, `fr.1`, `fu.1` and `fh.5` to a directory in `$MANPATH`.

For usage, see the supplied man pages.
[man.md](man.md) is available on the web.

