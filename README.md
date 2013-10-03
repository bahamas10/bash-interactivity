bash-interactivity
============

Utilities to work with bash while interactive

Usage
-----

### `args`

Print arguments as read from the command line after wordsplitting, taken from
http://mywiki.wooledge.org/Arguments

    $ args hello "how are" you
    3 args: <hello> <how are> <you>

### `cdir`

`cd` into the dirname of the last argument, useful for if you've ever tried
cd'ing into a file instead of a directory

    ~ $ cd dev/something/file.txt
    -bash: cd: file.txt: No such file or directory
    ~ $ cdir
    ~/dev/something $

### `parr`

Print a bash array by name

This uses `eval`, as that is the only way to reference an array
that has its name stored in a variable while retaining indices (for
associative and sparse arrays).
More info on why indirection won't work for this here
http://mywiki.wooledge.org/BashFAQ/006#Evaluating_indirect.2Freference_variables

Note: the output generated by this function is NOT safe to eval
by the shell, this is just meant to inspect the contents of array,
like `var_dump` in PHP, or `console.dir` in JavaScript

    $ a=([0]="hello" [1]="how are" [5]="you")
    $ parr a
    (
            [0]=`hello`
            [1]=`how are`
            [5]=`you`
    )

This will also work for associative arrays in Bash >= 4

    $ parr BASH_ALIASES
    (
            [urldecode]=`python -c 'import sys;import urllib as u;print u.unquote_plus(sys.stdin.read());'`
            [basher]=`~/.basher/basher`
            [joyentstillpaying]=`sdc-listmachines | json -a -c "state !== 'running'" name state`
            [gerp]=`grep`
            [lsdisks]=`kstat -lc disk :::class | field 3 :`
            [ls]=`ls -p --color=auto`
            [cdir]=`cd "${_%/*}"`
            [urlencode]=`python -c 'import sys;import urllib as u;print u.quote_plus(sys.stdin.read());'`
            [cpp2c]=`sed -e 's#//\(.*\)#/*\1 */#'`
            [externalip]=`curl -s http://ifconfig.me/ip`
            [l]=`ls -CF`
            [lsnpm]=`npm ls -g --depth=0`
            [chomd]=`chmod`
    )

Exports
-------

### Aliases

- `cdir`

### Functions

- `args`
- `parr`
- `_parr` (`parr` bash completion)

### Bash Completion

Provided for...

- `parr`

Installation
------------

### basher

Use [basher](https://github.com/bahamas10/basher) to manage this plugin

After installing `basher`, install this plugin by running

    basher install git://github.com/bahamas10/bash-interactivity.git

Or install manually for `basher` with

    cd ~/.basher/plugins
    git clone git://github.com/bahamas10/bash-interactivity.git

### manually

    git clone git://github.com/bahamas10/bash-interactivity.git
    cd bash-interactivity
    cat interactivity.bash >> ~/.bashrc
    exec bash

License
-------

MIT