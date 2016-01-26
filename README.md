# Char Menu

[![License GPL 3](https://img.shields.io/badge/license-GPL_3-green.svg)](http://www.gnu.org/licenses/gpl-3.0.txt)
[![Build Status](https://travis-ci.org/mrkkrp/char-menu.svg?branch=master)](https://travis-ci.org/mrkkrp/char-menu)

![gif animation here]

This package allows to insert arbitrary symbols in Emacs in a very efficient
and straightforward way. Whether you ever need to insert only a couple of
proper punctuation symbols or you're a Unicode geek who likes all sorts of
arrows and fancy math symbols, this package may be of some use.

Selling points:

* it allows you organize all symbols you ever need into a hierarchy you
  define;

* in that tree-like structure most frequently used commands will require
  only one key-press, while others may get dedicated section (for example,
  “arrows”) so you first select that section and then you choose a symbol in
  it;

* it makes sense to have paired characters in that menu, like `“”` (and for
  that matter arbitrary combinations of symbols);

* however insertion of paired characters will place the point between them;

* …and if you insert paired characters while some text is selected, they
  will wrap it.

## Various methods to insert a Unicode symbol in Emacs

*Coming soon…*

## Installation

For manual installation simply put the package on your `load-path` and then
add the following at the top of file where you would like to use the
package:

```emacs-lisp
(require 'char-menu)
```

## Usage

*Coming soon…*

## Example of configuration

*Coming soon…*

## License

Copyright © 2016 Mark Karpov

Distributed under GNU GPL, version 3.
