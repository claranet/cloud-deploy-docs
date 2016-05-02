.. title:README file


Read the doc
------------

    * git clone

    * open ``REPO PATH``/build/html/index.html in browser.

Edit page
---------

ReST syntax
___________

ReST syntax is text based as markdown or wiki language.

Install *sphinx*::

    virtualenv sphinx
    source sphinx/bin/activate
    pip install sphinx sphinx_rtd_theme

Edit the targeted file from ``source/rst/``::

    vim source/rst/api.rst

Follow sphinx documentation `online`_ or from your locally by installing the
following package::

    sudo apt-get install sphinx-doc

.. _online: http://www.sphinx-doc.org/en/stable/contents.html


Generate new doc::

    make html

Generate Epub::

    make html epub

You can read the generated doc from ``build/html/index.html``.

Edit from other format
______________________

Just write your doc in the any text format and mail it to Zied. He will convert 
it into ReST.

Create new page
---------------
::

    TODO

