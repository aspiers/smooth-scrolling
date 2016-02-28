# `smooth-scrolling.el`

## About

This package offers a minor mode which make emacs scroll smoothly.  It
keeps the point away from the top and bottom of the current buffer's
window in order to keep lines of context around the point visible as
much as possible, whilst minimising the frequency of sudden scroll
jumps which are visually confusing.

This is a nice alternative to all the native `scroll-*` custom
variables, which unfortunately cannot provide this functionality
perfectly.  For example, when using the built-in variables, clicking
with the mouse in the margin will immediately scroll the window to
maintain the margin, so the text that you clicked on will no longer be
under the mouse.  This can be disorienting.  In contrast, this mode
will not do any scrolling until you actually move up or down a line.

Also, the built-in margin code does not interact well with small
windows.  If the margin is more than half the window height, you get
some weird behavior, because the point is always hitting both the top
and bottom margins.  This package auto-adjusts the margin in each
buffer to never exceed half the window height, so the top and bottom
margins never overlap.

See also emacswiki's
[SmoothScrolling page](http://www.emacswiki.org/cgi-bin/wiki/SmoothScrolling)
for more information, although at the time of writing, its content
probably did more to confuse than enlighten.

## Installation

You have various options, including the following:

*   Install the [package](https://melpa.org/#/smooth-scrolling)
    from [MELPA](https://melpa.org/#/getting-started)
    (see this [friendly quickstart guide](http://ergoemacs.org/emacs/emacs_package_system.html))
*   Install via [`el-get`](https://github.com/dimitri/el-get/blob/master/README.md)
*   Simply download this repository and place the elisp file
    somewhere on your [`load-path`](https://www.emacswiki.org/emacs/LoadPath).

## Usage

To interactively toggle the mode on / off:

    M-x smooth-scrolling-mode

To make the mode permanent, put this in your .emacs:

    (require 'smooth-scrolling)
    (smooth-scrolling-mode 1)

## Difference with `smooth-scroll.el`

This package should not be confused with the similarly-named
[`smooth-scroll.el`](https://www.emacswiki.org/emacs/smooth-scroll.el),
which has similar goals but takes a different approach, requiring
navigation keys to be bound to dedicated
`scroll-{up,down,left,right}-1` functions.

## Notes

This only affects the behaviour of the `next-line` and `previous-line`
functions, usually bound to the cursor keys and `C-n`/`C-p`, and
repeated isearches (`isearch-repeat`).  Other methods of moving the
point will behave as normal according to the standard custom
variables.

Prefix arguments to `next-line` and `previous-line` are honored. The
minimum number of lines are scrolled in order to keep the point
outside the margin.

There is one case where moving the point in this fashion may cause a
jump: if the point is placed inside one of the margins by another
method (e.g. left mouse click, or `M-x goto-line`) and then moved in
the normal way, the advice code will scroll the minimum number of
lines in order to keep the point outside the margin.  This jump may
cause some slight confusion at first, but hopefully it is justified by
the benefit of automatically ensuring `smooth-scroll-margin` lines of
context are visible around the point as often as possible.

## TODO

-   Maybe add option to avoid scroll jumps when point is within margin.
-   Minimize the number of autoloads in the file.  Currently
    everything is marked as such.

## Authors

Originally written by Adam Spiers, it was made into a proper ELPA
package by Jeremy Bondeson, and later converted into a minor mode by
Ryan C. Thompson.

Thanks also to Mark Hulme-Jones and consolers on #emacs for helping
debug issues with line-wrapping in the original implementation.
