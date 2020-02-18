# Char Menu

[![License GPL 3](https://img.shields.io/badge/license-GPL_3-green.svg)](http://www.gnu.org/licenses/gpl-3.0.txt)
[![MELPA](https://melpa.org/packages/char-menu-badge.svg)](https://melpa.org/#/char-menu)
[![CircleCI](https://circleci.com/gh/mrkkrp/char-menu/tree/master.svg?style=svg)](https://circleci.com/gh/mrkkrp/char-menu/tree/master)

* [Various methods to insert a Unicode symbol in Emacs](#various-methods-to-insert-a-unicode-symbol-in-emacs)
* [Installation](#installation)
* [Usage](#usage)
* [Example of configuration](#example-of-configuration)
* [Visual appearance of the menu](#visual-appearance-of-the-menu)
* [License](#license)

This package allows to insert arbitrary symbols in Emacs in a very efficient
and straightforward way. Whether you ever need to insert only a couple of
proper punctuation symbols or you're a Unicode geek who likes all sorts of
arrows and fancy math symbols, this package may be of some use.

Features:

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

Let's skip copying characters from file or web-page—it's just too
inefficient.

One method to insert arbitrary characters is to use `key-translation-map`,
like this:

```emacs-lisp
(define-key key-translation-map (kbd "<menu> p") (kbd "φ"))
```

The main problem here is that if you have many such things, they are hard to
remember, and this approach is not very good at organizing symbols into
categories. The same with built-in key bindings like <kbd>C-x 8
…</kbd>—something I always had trouble using, they are also hard to type.

Another approach is to use `abbrev-mode`. I don't like that mode because you
need to keep it enabled and chances are even if you normally don't need the
word “alpha”, it does not mean that you want always replace it with the “α”
symbol. I like to be able to explicitly control when I want “alpha” and when
I want “α”.

Inserting a character by its name is done with the `insert-char` command,
but it cannot be used heavily because even with auto-completion it takes too
long to type full name of a character. Also, we usually don't want all
characters available, but a certain subset of them that is highly useful.

## Installation

For manual installation simply put the package on your `load-path` and then
add the following at the top of file where you would like to use the
package:

```emacs-lisp
(require 'char-menu)
```

However, the simplest method to install the package is with MELPA: <kbd>M-x
package-install char-menu RET</kbd>.

## Usage

Normally, there are only two things that you need to do:

1. Set the variable `char-menu`.
2. Bind the command `char-menu`.

The variable `char-menu` can be customized via the “customize” interface
(<kbd>M-x customize-group char-menu RET</kbd>) or set with `setq`. That
variable should be bound to a list where every element is either a string to
insert or a sub-menu, which is represented as a list where the first element
is the header of the sub-menu and the rest is its items.

Place most frequently needed characters at the beginning of the list. Other
characters can be organized in categories: “Arrows”, “Greek letters”, “Math
symbols”, whatever. It's best to keep the number of menu items less then 10,
because then you will be able to choose a character using a single key press
on home row. You don't need to think about key bindings—the package assigns
them for you.

Usually you want to insert a single character, but there is a need for
paired punctuation like “this” or «this». Just put these characters together
and they will be inserted with point (cursor) between them. Wrapping of
selected text is also supported.

As for binding of `char-menu` command, it should be as easy as:

```emacs-lisp
(global-set-key (kbd "<menu> SPC") #'char-menu)
```

Of course you can choose a different key combination to assign for this.

## Example of configuration

The default configuration is quite basic:

```emacs-lisp
("—" "‘’" "“”" "…")
```

As an example of something more sophisticated, try this:

```emacs-lisp
("—" "‘’" "“”" "…" "«»" "–"
 ("Typography" "•" "©" "†" "‡" "°" "·" "§" "№" "★")
 ("Math"       "≈" "≡" "≠" "∞" "×" "±" "∓" "÷" "√")
 ("Arrows"     "←" "→" "↑" "↓" "⇐" "⇒" "⇑" "⇓")
 ("Greek"      "α" "β" "Y" "δ" "ε" "ζ" "η" "θ" "ι" "κ" "λ" "μ"
               "ν" "ξ" "ο" "π" "ρ" "σ" "τ" "υ" "φ" "χ" "ψ" "ω"))
```

Except for Greek letters that are a bit too numerous, all characters here
can be accessed in one or two key strokes. Given that there is always a
visual clue before you and all the characters you need to type are on the
home row (thanks to Avy), this method of input is quite efficient.

## Visual appearance of the menu

Just like [`ace-popup-menu`](https://github.com/mrkkrp/ace-popup-menu), the
package is built on top of [`avy-menu`](https://github.com/mrkkrp/avy-menu),
which implements this handy Avy-powered popup menu. To control appearance of
the menu, invoke <kbd>M-x customize-group avy-menu RET</kbd>.

## License

Copyright © 2016–present Mark Karpov

Distributed under GNU GPL, version 3.
