# ATTN: This software is pre-alpha. It barely works. Keep that in mind. #

## Vim to Emacs ##

`vim_to_emacs` lets you easily switch between a set of files currently
open in `vim`, and open them automatically in `emacs`. At the moment,
this is a really, really basic way of opening those files in `emacs`
via `emacsclient` by parsing `~/.viminfo`.

## Usage ##

1. In vim: `:mksession`
2. At the command line (assuming `vim_to_emacs` is on your `PATH`): `vim_to_emacs`
3. Watch the magic unfold.

## Plans ##

I plan to provide `emacs_to_vim.el` which will let you take the open
buffers in `emacs` and open them in `vim`. I also plan to provide
`vim_to_emacs.vim` which will give you a handy way to do the
opposite.
