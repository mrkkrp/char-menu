# Char Menu

[![License GPL 3](https://img.shields.io/badge/license-GPL_3-green.svg)](http://www.gnu.org/licenses/gpl-3.0.txt)
[![MELPA](https://melpa.org/packages/char-menu-badge.svg)](https://melpa.org/#/char-menu)
![CI](https://github.com/mrkkrp/char-menu/workflows/CI/badge.svg?branch=master)

* [Various methods to insert a Unicode symbol in Emacs](#various-methods-to-insert-a-unicode-symbol-in-emacs)
* [Installation](#installation)
* [Usage](#usage)
* [Example of configuration](#example-of-configuration)
* [Visual appearance of the menu](#visual-appearance-of-the-menu)
* [License](#license)

This package allows the user to create a menu for fast insertion of
arbitrary symbols.

Features:

* The symbols can be organized in hierarchies.

* Most frequently used symbols require only one keystroke, while others are
  placed in dedicated sub-menus (for example, “arrows”) and can be inserted
  with two or three keystrokes.

* Paired characters like `“”` can be inserted. Normally, the point will be
  placed between the characters, but if some text is selected, the paired
  character will wrap it without moving the point.

## Various methods to insert a Unicode symbol in Emacs

Let's skip copying characters from a file or web-page—it is too inefficient.

One method to insert arbitrary characters is to use `key-translation-map`,
like this:

```emacs-lisp
(define-key key-translation-map (kbd "<menu> p") (kbd "φ"))
```

The main problem here is that if you have many such translations, they are
hard to remember. This approach is also not very good for organizing symbols
into categories.

Another approach is to use `abbrev-mode`. I don't like that mode because one
needs to keep it enabled and chances are even if you normally don't need the
word “alpha”, it does not mean that you always want to replace it with the
symbol “α”.

Inserting a character by its name is done with the `insert-char` command,
but it cannot be used heavily because even with auto-completion it takes too
long to type the full name of a character. Also, I usually don't want to
pick from all available characters, but rather from a subset of them.

## Installation

The package is available via MELPA, so you can just type `M-x
package-install RET char-menu RET`.

If you would like to install the package manually, download or clone it and
put on Emacs' `load-path`. Then you can require it in your init file like
this:

```emacs-lisp
(require 'char-menu)
```

## Usage

Normally, there are only two things that you need to do:

1. Set the variable `char-menu`.
2. Bind the command `char-menu`.

The variable `char-menu` can be customized via the “customize” interface
(`M-x customize-group char-menu RET`) or set with `setq`. That variable
should be bound to a list where every element is either a string to insert
or a sub-menu, which is represented as a list where the first element is the
header of the sub-menu and the rest is its items.

Place the most frequently needed characters at the beginning of the list.
Other characters can be organized in categories: “Arrows”, “Greek letters”,
“Math symbols”, whatever. It's best to keep the number of the menu items
less then 10, because then you will be able to choose a character using a
single key press on the home row. You don't need to think about key
bindings—the package assigns them for you.

Usually you want to insert a single character, but there is a need for
paired punctuation like “this” or «this». Just put these characters together
and they will be inserted with point (cursor) between them. Wrapping of
selected text is also supported.

As for binding of the `char-menu` command, it should be as easy as:

```emacs-lisp
(global-set-key (kbd "<menu> SPC") #'char-menu)
```

Of course you can choose a different key combination.

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
can be accessed in one or two key strokes.

## Visual appearance of the menu

Just like [`ace-popup-menu`](https://github.com/mrkkrp/ace-popup-menu), the
package is built on top of [`avy-menu`](https://github.com/mrkkrp/avy-menu),
which implements a handy Avy-powered popup menu. To control appearance of
the menu, invoke `M-x customize-group avy-menu RET`.

## License

Copyright © 2016–present Mark Karpov

Distributed under GNU GPL, version 3.
