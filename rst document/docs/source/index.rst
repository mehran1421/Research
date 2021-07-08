SublimeText ♥ reStructuredText
==============================
"""""""""""""""""
Document Title
"""""""""""""""""
...........
Subtitle
...........

.. contents:: Overview
   :depth: 3

===================
Section 1
===================

Text can be *italicized* or **bolded**  as well as ``monospaced``.
You can \*escape certain\* special characters.

----------------------
Subsection 1 (Level 2)
----------------------

Some section 2 text

Sub-subsection 1 (level 3)
--------------------------

Some more text.

=========
Examples
=========

--------
Comments
--------

.. This is a comment
   Special notes that are not shown but might come out as HTML comments

------
Images
------

Add an image with:

.. image:: screenshots/file.png
   :height: 100
   :width: 200
   :alt: alternate text

You can inline an image or other directive with the |customsub| command.

.. |customsub| image:: image/image.png
              :alt: (missing image text)

-----
Lists
-----

- Bullet are made like this
- Point levels must be consistent
    * Sub-bullets
        + Sub-sub-bullets
- Lists

Term
    Definition for term
Term2
    Definition for term 2

:List of Things:
    item1 - these are 'field lists' not bulleted lists
    item2
    item 3

:Something: single item
:Someitem: single item

-----------------
Preformatted text
-----------------

A code example prefix must always end with double colon like it's presenting something::

    Anything indented is part of the preformatted block
   Until
  It gets back to
 Allll the way left

Now we're out of the preformatted block.

------------
Code blocks
------------

There are three equivalents: ``code``, ``sourcecode``, and ``code-block``.

.. code:: python

   import os
   print(help(os))

.. sourcecode::

  # Equivalent

.. code-block::

  # Equivalent

-----
Links
-----

Web addresses by themselves will auto link, like this: https://www.devdungeon.com

You can also inline custom links: `Google search engine <https://www.google.com>`_

This is a simple link_ to Google with the link defined separately.

.. _link: https://www.google.com

This is a link to the `Python website`_.

.. _Python website: http://www.python.org/

This is a link back to `Section 1`_. You can link based off of the heading name
within a document.

---------
Footnotes
---------

Footnote Reference [1]_

.. [1] This is footnote number one that would go at the bottom of the document.

Or autonumbered [#]

.. [#] This automatically becomes second, based on the 1 already existing.

-----------------
Lines/Transitions
-----------------

Any 4+ repeated characters with blank lines surrounding it becomes an hr line, like this.

====================================

------
Tables
------

+--------+--------+--------+
| Time   | Number | Value  |
+========+========+========+
| 12:00  | 42     | 2      |
+--------+--------+--------+
| 23:00  | 23     | 4      |
+--------+--------+--------+

----------------------
Preserving line breaks
----------------------

Normally you can break the line in the middle of a paragraph and it will
ignore the newline. If you want to preserve the newlines, use the ``|`` prefix
on the lines. For example:

| These lines will
| break exactly
| where we told them to.


.. toctree::

   whatsnew/index.rst
   tutorial/index.rst
   faq/index.rst
   glossary.rst

   about.rst
   bugs.rst
   copyright.rst
   license.rst

Demo
----

(image links to a Youtube video)

.. image:: http://img.youtube.com/vi/otM_tjIi_vY/0.jpg
   :target: http://www.youtube.com/watch?v=otM_tjIi_vY



.. contents::
   :depth: 2
   :local:


Install
-------

The easiest way to install is via `Sublime Package Control <http://wbond.net/sublime_packages/package_control>`_ . Just look for *"Restructured Text (RST) Snippets"*

Otherwise you can:

- Clone the repository into
  your `packages folder <http://sublimetext.info/docs/en/basic_concepts.html#the-packages-directory>`_::

      git clone git@github.com:mgaitan/sublime-rst-completion.git

- Or download the `.zip`_ file and unzip it into your ST2/ST3 packages
  directory.

Optionally, to use the `Render preview`_ feature, you need to install at least one of
Pandoc_, docutils_ or rst2pdf_ and they should be accessible in your ``PATH``. (Copy the ``command_path`` variable from the package's settings file to your user settings file and add paths to your local installations to it.)  In debian/ubuntu you can install them via ``apt-get``::

    $ sudo apt-get install pandoc docutils rst2pdf

.. _Pandoc: http://johnmacfarlane.net/pandoc/
.. _rst2pdf: http://rst2pdf.ralsina.com.ar/
.. _docutils: http://docutils.sourceforge.net/

Usage
-----

Simple snippets work as tab-triggered shortcuts: type the shortcut and press ``<TAB>`` to
replace it with the snippet. If the snippet has placeholders, you can jump between them
using tab.

+------------------------+------------------------------------+----------------------------+
| shortcut               | result                             | key binding                |
+========================+====================================+============================+
| ``h1``                 | Header level 1                     | see `Headers`_             |
+------------------------+------------------------------------+----------------------------+
| ``h2``                 | Header level 2                     |                            |
+------------------------+------------------------------------+----------------------------+
| ``h3``                 | Header level 3                     |                            |
+------------------------+------------------------------------+----------------------------+
| ``e``                  | emphasis                           | ``ctrl+alt+i``             |
|                        |                                    | (``super+shift+i`` on Mac) |
+------------------------+------------------------------------+----------------------------+
| ``se``                 | strong emphasis (bold)             | ``ctrl+alt+b``             |
|                        |                                    | (``super+shift+b`` on Mac) |
+------------------------+------------------------------------+----------------------------+
| ``lit`` or ``literal`` | literal text (inline code)         | ``ctrl+alt+k``             |
|                        |                                    | (``super+shift+k`` on Mac) |
+------------------------+------------------------------------+----------------------------+
| ``list``               | unordered list                     | see `Smart Lists`_         |
+------------------------+------------------------------------+----------------------------+
| ``listn``              | ordered list                       |                            |
+------------------------+------------------------------------+----------------------------+
| ``listan``             | auto ordered list                  |                            |
+------------------------+------------------------------------+----------------------------+
| ``def``                | term definition                    |                            |
+------------------------+------------------------------------+----------------------------+
| ``code``               | code-block directive (sphinx)      |                            |
+------------------------+------------------------------------+----------------------------+
| ``source``             | preformatted (``::`` block)        |                            |
+------------------------+------------------------------------+----------------------------+
| ``img``                | image                              |                            |
+------------------------+------------------------------------+----------------------------+
| ``fig``                | figure                             |                            |
+------------------------+------------------------------------+----------------------------+
| ``table``              | simple table                       | ``ctrl+t`` see `Magic      |
|                        |                                    | Tables`_                   |
+------------------------+------------------------------------+----------------------------+
| ``link``               | refered hyperlink                  |                            |
+------------------------+------------------------------------+----------------------------+
| ``linki``              | embeded hyperlink                  |                            |
+------------------------+------------------------------------+----------------------------+
| ``fn`` or ``cite``     | autonumbered footnote or cite      | ``alt+shift+f`` see        |
|                        |                                    | `Magic Footnotes`_         |
+------------------------+------------------------------------+----------------------------+
| ``quote``              | Quotation (``epigraph`` directive) |                            |
+------------------------+------------------------------------+----------------------------+

Also standard admonitions are expanded:

+---------------+
| shortcut      |
+===============+
| ``attention`` |
+---------------+
| ``caution``   |
+---------------+
| ``danger``    |
+---------------+
| ``error``     |
+---------------+
| ``hint``      |
+---------------+
| ``important`` |
+---------------+
| ``note``      |
+---------------+
| ``tip``       |
+---------------+
| ``warning``   |
+---------------+

Render preview
--------------

You can preview your document in different formats converted with different tools
pressing ``ctrl+shift+r``.

The *Quick Window* will offer the format and tool and the result will be automatically open
after the conversion.

By the moment, it can use Pandoc_, rst2pdf_, or ``rst2*.py`` tools (included with
docutils_) to produce ``html``, ``pdf``, ``odt`` or ``docx`` output formats.

Each time you select a ``format + tool`` option, it turns the default the following times.

.. note::

    The original code is from the `SublimePandoc <https://github.com/jclement/SublimePandoc>`_
    project.


Magic Tables
------------

There is a particular *magic* expansion for tables. Here is how it works:

Grid table
++++++++++

1. Create some kind of table outline, separating column with two or more spaces::


      This is paragraph text *before* the table.

      Column 1  Column 2
      Foo  Put two (or more) spaces as a field separator.
      Bar  Even very very long lines like these are fine, as long as you do not put in line endings here.

      This is paragraph text *after* the table.

2. Put your cursor somewhere in the content to convert as table.
3. Press ``ctrl+t, enter`` (Linux or Windows) or ``super+shift+t, enter`` (Mac). The output will look
   something like this::

      This is paragraph text *before* the table.

      +----------+---------------------------------------------------------+
      | Column 1 | Column 2                                                |
      +==========+=========================================================+
      | Foo      | Put two (or more) spaces as a field separator.          |
      +----------+---------------------------------------------------------+
      | Bar      | Even very very long lines like these are fine, as long  |
      |          | as you do not put in line endings here.                 |
      +----------+---------------------------------------------------------+

      This is paragraph text *after* the table.


Now suppose you add some text in a cell::

      +----------+---------------------------------------------------------+
      | Column 1 | Column 2                                                |
      +==========+=========================================================+
      | Foo is longer now     | Put two (or more) spaces as a field separator.          |
      +----------+---------------------------------------------------------+
      | Bar      | Even very very long lines like these are fine, as long  |
      |          | as you do not put in line endings here.                 |
      +----------+---------------------------------------------------------+

Press the same trigger: magically, the structure will be fixed::


      +-------------------+--------------------------------------------------------+
      | Column 1          | Column 2                                               |
      +===================+========================================================+
      | Foo is longer now | Put two (or more) spaces as a field separator.         |
      +-------------------+--------------------------------------------------------+
      | Bar               | Even very very long lines like these are fine, as long |
      |                   | as you do not put in line endings here.                |
      +-------------------+--------------------------------------------------------+


In addition, if you would like to keep the column width fixed, you could **reflow** the table pressing ``ctrl+t, r`` (``super+shift+t, r`` in Mac). The result would be this::


      +----------+---------------------------------------------------------+
      | Column 1 | Column 2                                                |
      +==========+=========================================================+
      | Foo is   | Put two (or more) spaces as a field separator.          |
      | longer   |                                                         |
      | now      |                                                         |
      +----------+---------------------------------------------------------+
      | Bar      | Even very very long lines like these are fine, as long  |
      |          | as you do not put in line endings here.                 |
      +----------+---------------------------------------------------------+

With the base trigger combination and the cursors you can merge simple cells.
For example, suppose you have this table::

    +----+----+
    | h1 | h2 |
    +====+====+
    | 11 | 12 |
    +----+----+
    | 21 | 22 |
    +----+----+

Move the cursor to the cell ``12`` and press ``ctrl+t, down``. You'll get this::

    +----+----+
    | h1 | h2 |
    +====+====+
    | 11 | 12 |
    +----+    |
    | 21 | 22 |
    +----+----+


.. note::

   The original code of this feature was taken from
   `Vincent Driessen's vim-rst-tables <https://github.com/nvie/vim-rst-tables>`_ :

.. note::

   The original code of `wcwidth <https://github.com/jquast/wcwidth>`_ was taken to solve alignment issue with CJK characters.

Simple table
++++++++++++

Instead of tables above, a simpler style table is also supported. Here is how it works:

1. Create some kind of table outline, separating column with two or more spaces::


      This is paragraph text *before* the table.

      Column 1  Column 2
      Foo  Put two (or more) spaces as a field separator.
      Bar  Even very very long lines like these are fine, as long as you do not put in line endings here.

      This is paragraph text *after* the table.

2. Put your cursor somewhere in the content to convert as table.
3. Press ``ctrl+t, s`` (Linux or Windows) or ``super+shift+t, s`` (Mac). The output will look
   something like this::

      This is paragraph text *before* the table.

      ==========  ================================================================================================
      Column 1    Column 2
      ==========  ================================================================================================
      Foo         Put two (or more) spaces as a field separator.
      Bar         Even very very long lines like these are fine, as long as you do not put in line endings here.
      ==========  ================================================================================================

      This is paragraph text *after* the table.


Now suppose you add some text in a cell::


      ==========  ================================================================================================
      Column 1    Column 2
      ==========  ================================================================================================
      Foo is longer now         Put two (or more) spaces as a field separator.
      Bar         Even very very long lines like these are fine, as long as you do not put in line endings here.
      ==========  ================================================================================================

Press the same trigger: magically, the structure will be fixed::


      ===================  ================================================================================================
      Column 1             Column 2
      ===================  ================================================================================================
      Foo is longer now    Put two (or more) spaces as a field separator.
      Bar                  Even very very long lines like these are fine, as long as you do not put in line endings here.
      ===================  ================================================================================================


.. note::

   The original code of this feature was taken from
   `Vincent Driessen's vim-rst-tables <https://github.com/nvie/vim-rst-tables>`_ :

Smart lists
-----------


Ordered or unordered lists patterns are automatically detected. When you type something
like this::

  1. Some item
  2. Another|

When press ``enter`` the newline will prepended with a logical next item::

  ...
  2. Another
  3. |

If you press ``enter`` when the item is empty, the markup is erased keeping
the same indent as the previous line, in order to allow multilines items.
Also note that orderer list works with an alphabetic pattern or roman numbers pattern
suffixed with a period
(``a. b. c. ...``, ``A. B. C. ...``, ``i. ii. iii. iv. ...``, ``X. XI. XII. ...``, ``#.``);
surrounded by parentheses
(``(a) (b) (c) ...``, ``(A) (B) (C) ...``, ``(i) (ii) (iii) (iv) ...``, ``(X) (XI) (XII) ...``, ``(#)``);
or suffixed with a right-parenthesis.
(``a) b) c) ...``, ``A) B) C) ...``, ``i) ii) iii) iv) ...``, ``X) XI) XII) ...``, ``#)``);

.. tip::

   The very same feature works for  `line blocks <http://docutils.sourceforge.net/docs/ref/rst/restructuredtext.html#line-blocks>`_ starting a line with ``|``.

.. note::

   This feature was proudly stolen from `Muchenxuan Tongh's SmartMarkdown
   <https://github.com/demon386/SmartMarkdown>`_


Headers
--------

.. _header completion:

Autocompletion
+++++++++++++++

You can autocomplete standard headers (over/)underlines with ``TAB``.

For example try this::


    **********<TAB>
    A longer main title
    *******

Or this::

    A subtitle
    ---<TAB>


You'll get::


    *******************
    A longer main title
    *******************

    A subtitle
    ----------

respectively.

Folding/unfolding
+++++++++++++++++

If you put the cursor in a completed header and press ``shift + TAB`` (``alt + TAB`` in Mac),
the section under it will be folded/unfolded.

For example::

    Folding/unfolding
    +++++++++++++++++<TAB>

    If you put the cursor in a completed header and press ``shift + TAB``,
    (``alt + TAB`` in Mac) the section under it will be folded/unfolded.

    Navigation
    ++++++++++

    ...

Result in:

    .. image:: https://raw.github.com/dbousamra/sublime-rst-completion/11_foldable_headers/img/folding.png


Nested sections under a header are included.


Navigation
++++++++++

Also, it's possible to jump between headers.
``alt+down`` and ``alt+up`` move the cursor position to the closer next or
previous header respectively.

``alt+shift+down`` and ``alt+shift+up`` to the same, but only between headers
with the same or higher level (i.e. ignore childrens)

The header level is detected automatically.


Adjust header level
+++++++++++++++++++

With the cursor in a header, press ``ctrl + +`` (plus key) and ``ctrl + -``
(minus key) (``alt + +`` and ``alt + -``, in Mac) will increase and decrease the
header level respectively. The adornment decoration (underline / overline) are
autodetected from the document and uses Sphinx's conventions as default.

For example, you have the cursor in::

    Magic Footnotes|
    ---------------

Which is a header level 2 and want to convert to a level 3, press ``ctrl + -`` to get::

    Magic Footnotes
    +++++++++++++++
    |


Magic Footnotes
---------------

This is the smarter way to add footnotes, grouping them (and keepping count)
in a common region at the bottom of the document.

When you want to add a new note, press ``alt+shift+f``.
This will happen:

-  A new ``n+1`` (where ``n`` is the current footnotes count) note reference
   will be added in the current cursor position
-  The corresponding reference definition will be added
   at the bottom of the *footnotes region*
-  The cursor will be moved to write the note

After write the note you can go back to the reference with ``shift+up``. Also, if
the cursor is just after a reference (i.e: the caret is next to the underscore like this ``[XX]_|`` ) you can jump to its definition with ``shift+down`` [1]_.

This feature is based on the code by `J. Nicholas Geist <https://github.com/jngeist>`_
for `MarkdownEditing <https://github.com/ttscoff/MarkdownEditing>`_

Authors
-------

- Most features added by Martín Gaitán (`mgaitan <http://github.com/mgaitan>`_)
- Original idea by Dominic Bou-Samra (`dbousamra`_)
- And some kind contributors_

.. tip::

    Pull requests and bug reports are welcome!

License
-------

It's under a `BSD license <https://github.com/dbousamra/sublime-rst-completion/blob/master/LICENSE>`_ .



.. _.zip: http://github.com/dbousamra/sublime-rst-completion/zipball/master
.. _dbousamra: http://github.com/dbousamra
.. _contributors: https://github.com/dbousamra/sublime-rst-completion/contributors

.. [1]  in fact, you can also jump forward and back between notes with
        the general ``alt+shift+f``
