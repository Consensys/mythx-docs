# Contributing to the MythX documentation

## Keep things concise

This guide aims to provide information on MythX based on whether you are a user, tool developer, or partner. We strive to find a good compromise between precise technical language and description with examples to make the documentation as accessible as possible. Try to make a reasonable effort in both directions.

## Don't sell

This guide does not aim to sell the MythX platform to anyone. Instead, the goal is to help users get started as quickly as possible in using the platform, and also give developers the tools they need to start building on the platform. While we appreciate the fandom, we believe that the product can sell itself. :blush:

## Match organization

Your contributions will be much more useful and successful if it is located where one would expect it, and in the form that one would expect it. So please try to match the organization of the existing documentation, be it page structure or location in the table of contents.

In general, unless your topic is truly new, please do not add any new pages but instead try to fit your work into the existing ones.

A notable exception to this rule is for new libraries and tools. If you would like to submit a new library or tool for inclusion in our documentation, please create a document in `docs/source/tooling/<toolname>.rst`.

## Formatting

The documentation is written in [reStructuredText](http://docutils.sourceforge.net/docs/user/rst/quickref.html) (RST) and is built with [Sphinx](http://www.sphinx-doc.org). As this is a very flexible format, we have come up with some format guidelines to keep the source files readable and uniform.

### Headings

There are three orders of headings in the documentation. A heading of first order should be underlined with `=`, second order with `-` and third order with `^`. Example:

```reStructuredText
Heading 1
=========

...

Heading 2
---------

...

Heading 3
^^^^^^^^^

...
```

Please add two empty lines before a heading and one after it to make the source more readable and quick to navigate.

### Code blocks

When providing code samples (which is strongly encouraged), make sure to annotate your code blocks with the correct syntax highlighting tag. Examples:

```reStructuredText
.. code-block:: javascript

   Some Ruby code.
```

```reStructuredText
.. code-block:: console

   Some console commands
```

If your content truly needs no syntax highlighting, you can use a double-colon `::`. For example:

```reStructuredText
Here is some monospaced text::

  Monospaced text goes here.
```

Make sure to include the newline before and after the `code-block` instruction to make sure it's valid syntax. Also, indentation is significant and important.

For more details and the languages supported by the syntax highlighter (pygments), please see the [Sphinx documentation](http://www.sphinx-doc.org/en/1.8/markup/code.html#directive-code-block).

### Page titles and references

Please put an anchor at the top of all pages. It should be in the form of `.. _section.page`.

You can link to this page in your text by encoding the reference as `` :ref:`section.page` ``.

## Thanks for contributing!
Here's your reward in the form of a cute cat picture.
![](docs/source/_static/cat.jpeg)
