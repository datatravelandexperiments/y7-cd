# y7 cd

A directory stack for
[y7](https://codeberg.org/datatravelandexperiments/y7).

## Shell functions

### cd

`cd` …

Changes directory, with indexing or search in the directory stack.

If the argument(s) are accepted by builtin `cd`, changes directory
according to those arguments.

If the argument is `-`_n_, changes to the _n_^th^ directory from the
start of the start of the directory stack. (This is 0 based, as `-0`
is assumed to be the working directory).

If the argument is `+`_n_, changes to the _n_^th^ directory from the
end of the directory stack (1 based, so `+1` is the last in the stack).

Otherwise, searches the stack for an entry that contains the
argument as part of its path. If one is found, changes to that directory.
Prefers a match at the end of the path; for example, `cd src` will prefer
`/usr/local/src` over `/usr/local/src/y7` regardless of its position
in the list. Otherwise prefers an earlier match.

In any case, the new working directory becomes the top of the stack.
If it previously appeared in the stack, that entry is removed.
The previous working directory becomes the next entry in the stack,
and so on. (This is [`pushd`](#pushd) functionality.)

### dirs

`dirs` [-elspv] [-A array] [-S var] [dir:dir:…]

Prints the directory stack.

By default, the output includes the `-`/`+` indices that can be used
as argument to [`cd`](#cd). The `-s` option suppresses this.

By default, directories are shown with `~` for any directory under `$HOME`.
The `-l` option suppresses this, printing the full path.

This can also be used to display `$PATH`-style ‘:’-separated lists
in the same form, e.g. `dirs "$PATH"` or `dirs -S PATH`.

### dirsedit

Opens the directory stack in the configured editor (`$VISUAL` or `$EDITOR`).
The stack will be replaced by the edited list when the editor returns.
Note that this does **not** change directory to the new top of the stack.

Can also be used to edit `PATH` and similar variables, e.g. `dirsedit -S PATH`.

### pd

`pd` …

Prints the directory that [`cd`](#cd) would change to, given the same arguments.
This can be used to get the value of an entry in the directory stack.

### popd

`popd`

Changes to the next directory on the stack,
removing the working (top) directory.

### pushd

`pushd` …

Same as [`cd`](#cd), which also pushes the previous working directory.

### setd

`setd` …

Changes directory, like [`cd`](#cd), but _replaces_ the previous working
directory in the stack, rather than pushing it.
