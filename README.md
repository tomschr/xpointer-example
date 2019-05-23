# XInclude and XPointer example

An Example with XInclude and XPointer and how to reference them using IDs.

Process the file with:

    $ xmllint --xinclude article.xml

The file `article.xml` contains different XIncludes and XPointers:

* `xi:include href="author.xml" xpointer="xpointer(element(/1)/*)"/>`

   This is kind of what we know from SLE. Here it means: Include
   the "author.xml" file, start with the root element and return all
   children

* `<xi:include href="author.xml" xpointer="xpointer(id('author')/*)"/>`

   Includes the file `author.xml`, points to the element with the `xml:id`
   "author" (that would be `<author>`, the root element), and return
   all children.

* `xi:include xpointer="xpointer(id('editor')/*)"/>`

   This is something special: it doesn't have an href attribute! That
   means, it points to the current document (which is `article.xml`).
   The XPointer points to the element with the `xml:id` "editor" and
   returns all it's children.

* `<xi:include href="intro.xml" xpointer="xmlns(d=http://docbook.org/ns/docbook)xpointer(id('sec.intro')/*[not(self::d:title)])"/>`

   Includes the file `intro.xml`, and points to the section with the
   `xml:id` "sec.intro". Include all elements except the `title` element.
   Useful if you want to specify another title. Use sparingly!
   (The `xmlns()` expression is needed to define the DocBook 5 namespace
   for the XPointer.)
