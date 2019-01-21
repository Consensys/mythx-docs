Developer Guide Contribution Guidelines
=======================================


## 1. Keep Things Concise
The developer guide aims to provide dense information on MythX - whether you are a partner, tool developer or open-source maintainer. We try to find a good compromise between precise technical language and descriptive parts with examples to make the documentation more accessible. Try to make a reasonable effort in both directions.

## 2. Not a Marketing Document
Keep in mind that this is not a marketing document. The developer guide does not aim to sell the MythX platform to anyone. Instead, the goal is to help developers get started as quickly as possible in testing out the platform and playing around with the technology we have come up with. Please keep the fandom within reasonable boundaries. Of course that doesn't mean you can't have some fun here and there. :)

## 3. Format Guidelines
The documentation is written in reStructuredText. As RST is a very flexible format, we have come up with some format guidelines to keep the source files readable and uniform.

#### Headings
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

#### Code Blocks
When providing samples (which is strongly encouraged), make sure to annotate your code blocks with the correct syntax highlighting tag. Example:

```reStructuredText
.. code-block:: ruby

   Some Ruby code.
```

Don't forget the newline before and after the `code-block` instruction to make sure it's valid RST. For more details and the languages supported by the syntax highlighter (pygments), check out the [Sphinx documentation](http://www.sphinx-doc.org/en/1.5/markup/code.html#directive-code-block).

#### Document Structure
The guide aims to be easy to navigate. A developer should not have to click more than two links to see the first bits of code samples they're interested in, but a partner should also not be swamped with technical documentation that is irrelevant for them. We try to reflect all potential use cases in the document hierarchy. Unless absolutely necessary, please do not add any new documents but instead try to fit your work into the already existing ones.

A notable exception to this rule are JavaScript libraries and tools, simply because we have so many entries already. If you want to submit another one, you can create a document in `docs/source/tooling/<toolname>.rst` and add it to the index of the JavaScript section in `docs/source/main/mythx-for-developers.rst`.

## 4. Thanks for Contributing!
Here's your reward in the form of a cute cat picture.
![](docs/source/_static/cat.jpeg)
