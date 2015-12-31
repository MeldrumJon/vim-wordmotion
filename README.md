Customizable word motions for Vim
=================================

This is one word under Vim's definition:

```
CamelCaseACRONYMWords_underscore1234
^
```

With this plugin, this becomes 9 words:

```
CamelCaseACRONYMWords_under_score1234
^    ^   ^      ^    ^^    ^^    ^
```

Customization
=============

Set `g:wordmotion_prefix` if you don't like having the default word motions
(`w`, `b`, `e`, `ge`, `aw`, `iw`) hijacked.  
E.g.,
```
let g:wordmotion_prefix = "\<Leader>"
```

Define additional `word`s with `g:wordmotion_extra`.  
E.g., to treat `<WordsInAngleBrackets>` and `|WordsInPipes|` as single words:
```
let g:wordmotion_extra = [ "<\a\+>", "|\a\+|" ]
```
NOTE: this takes precedence over any existing `word` definitions.

The existing `word` definitions are:

| `word`                          | Example             |
|:--------------------------------|:--------------------|
| Camel case words                | `[Camel][Case]`     |
| Acronyms                        | `[HTML]And[CSS]`    |
| Regular words                   | `[regular] [words]` |
| Hexadecimal literals            | `[0x00ffFF] [0x0f]` |
| Binary literals                 | `[0b01] [0b0011]`   |
| Regular Numbers                 | `[1234] [5678]`     |
| Other keywords (`iskeyword`)    | `foo[_]bar`         |
| Other non-whitespace characters | `[~!@#$]`           |

Caveats
=======

There are some special cases with how Vim's word motions work. Not sure if
they should be reproduced in this plugin.  
E.g.,
```
Vim:

	^foo [b]ar$ -> dw -> ^foo[ ]$
	^ baz$               ^ baz$

	^[f]oo bar$ -> cw -> ^[ ]bar$

This plugin:

	^foo [b]ar$ -> dw -> ^foo [b]az$
	^ baz$

	^[f]oo bar$ -> cw -> ^[b]ar$
```
This plugin faithfully follows the motion of `w`, while Vim replaces these two
special cases with the behavior of `de` and `ce`, respectively.

TODO
====

* Detect if there are existing selections, and the direction of the existing
  selection. If the selection is backwards, `iw` needs to go backwards as well.
  If the current selection is contained within a word, expand to that word,
  otherwise, keep the other end of the selection.

Related
=======
[camelcasemotion](http://www.vim.org/scripts/script.php?script_id=1905)
