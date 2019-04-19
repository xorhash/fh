FL(1) - General Commands Manual

# NAME

**fl** - show of file history

# SYNOPSIS

**fl**
*file*

# DESCRIPTION

The
**fl**
utility shows the file history for
*file*.

The history contains the revision number,
the date when the revision was checked in and
the revision comment.

For the format of the file history,
see
fh(5).

# FILES

*H/H.*&zwnj;*file*

> the path to the file history

# EXIT STATUS

The **fl** utility exits&#160;0 on success, and&#160;&gt;0 if an error occurs.

# SEE ALSO

fr(1),
fu(1),
fh(5)

---

FR(1) - General Commands Manual

# NAME

**fr** - retrieve old version of file from history

# SYNOPSIS

**fr**
\[**-o**&nbsp;*filename*]
\[**-r**&nbsp;*revision*]
*file*

# DESCRIPTION

The
**fr**
utility fetches the most recent version of the given
*file*
from the file history.
If
*file*
already exists,
a warning is printed.

The following options are available:

**-o** *filename*

> Write to the given
> *filename*
> instead of
> *file*.
> This can be used to compare changes between two revisions.

**-r** *revision*

> Fetch the given
> *revision*
> instead of the most recent one.
> If this exceeds the most recent revision,
> the most recent revision is fetched anyway.
> Do not prefix
> *revision*
> with
> "r".

For the format of the file history,
see
fh(5).

# FILES

*H/H.*&zwnj;*file*

> the path to the file history

# EXIT STATUS

The **fr** utility exits&#160;0 on success, and&#160;&gt;0 if an error occurs.

# SEE ALSO

fl(1),
fu(1),
fh(5)

---

FU(1) - General Commands Manual

# NAME

**fu** - update file history

# SYNOPSIS

**fu**
*file*

# DESCRIPTION

The
**fu**
utility updates the file history.
The given
*file*
must be a non-empty file, not a directory or device.
It may not contain the sequence
"^AC"
at the beginning of any line;
on some platforms,
lines must not consist of a lone dot (.), either.
The given
*file*
must also not be a binary file.
The defintion of what constitutes a binary file depends on
diff(1).

A prompt
"comments? (EOF to end)"
is shown on update.
This can be used to indicate information about what changes were
made and why.
No such prompt is shown for the initial revision.
Do not enter a line that that starts with the sequence
"^AC".
Doing so will break the history file.

The file history will not be updated if the given
*file*
is equal to the most recent entry in the file history.

For the format of the file history,
see
fh(5).

# FILES

*H/H.*&zwnj;*file*

> the path to the file history

# EXIT STATUS

The **fu** utility exits&#160;0 on success, and&#160;&gt;0 if an error occurs.

# SEE ALSO

fl(1),
fr(1),
fh(5)

---

FH(5) - File Formats Manual

# NAME

**fh** - format of file histories

# DESCRIPTION

A file history file is a plaintext file.
It consists of two parts:
a sequence of
ed(1)
scripts and
a sequence of commit descriptions.

The
ed(1)
scripts are generated using
**diff -e**.

The commit descriptions consist of at least three lines:
a heading, the date and the commit message.
The heading consists of an ASCII SOH (start of heading;
&#92;001) followed by
'C',
a space,
the line number where the respective
ed(1)
script starts,
a comma and
the line number where the respective
ed(1)
script ends.
The date consists of the output of
date(1).
The commit message is a free-form text that continues on until
the next heading;
it may consist of multiple lines and it may just consist of
a single empty line.
A commit may look something like this:

	^AC 31,33
	Fri Apr 19 18:36:47 CEST 2019
	lowercase 'w'
	
	Grammatically, "world" in "Hello, world!" should be lowercase.

The first
ed(1)
script describes how to reconstruct the first file checked in with
fu(1).
Every subsequent script records the changes to the original.

History files are stored in a path named as follows:
*H/H.*&zwnj;*file*.
The
*H*
directory is always relative to the current directory.

# SEE ALSO

fl(1),
fr(1),
fu(1)

# BUGS

Because the
"base"
revision is the oldest one,
**the more history is recorded, the slower retrieval becomes**.
It may be worthwhile to archive or delete history files that go back
more than a few dozen of changes.

