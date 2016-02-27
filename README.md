# `smooth-scrolling.el`

## About

This package is a version of smooth-scrolling.el originally written by
[Adam Spiers](http://adamspiers.org/) that has been modified to be
loaded from `package.el`.

Make emacs scroll smoothly, keeping the point away from the top and
bottom of the current buffer's window in order to keep lines of
context around the point visible as much as possible, whilst
avoiding sudden scroll jumps which are visually confusing.

This is a nice alternative to all the native `scroll-*` custom
variables, which unfortunately cannot provide this functionality
perfectly.  `scroll-margin` comes closest, but has some bugs
(e.g. with handling of mouse clicks).  See
[Smooth Scrolling](http://www.emacswiki.org/cgi-bin/wiki/SmoothScrolling)
for the gory details.

## Installation

Put somewhere on your `load-path` and include

    (require 'smooth-scrolling)
    (smooth-scrolling-mode 1)
in your initialization file.  To turn it on or off, use
`M-x smooth-scrolling-mode`.

## Notes

This only affects the behaviour of the `next-line` and
`previous-line` functions, usually bound to the cursor keys and
`C-n`/`C-p`, and repeated isearches (`isearch-repeat`).  Other methods
of moving the point will behave as normal according to the standard
custom variables.

Prefix arguments to `next-line` and `previous-line` are
honored. The minimum number of lines are scrolled in order to keep the
point outside the margin.

There is one case where moving the point in this fashion may cause
a jump: if the point is placed inside one of the margins by another
method (e.g. left mouse click, or `M-x goto-line`) and then moved in
the normal way, the advice code will scroll the minimum number of
lines in order to keep the point outside the margin.  This jump may
cause some slight confusion at first, but hopefully it is justified
by the benefit of automatically ensuring `smooth-scroll-margin`
lines of context are visible around the point as often as possible.
