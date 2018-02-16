.. title:README file

Claranet Cloud Deploy documentation
===================================

Read the documentation
----------------------

HTML built version is available online at https://docs.cloud-deploy.io/

Edit the documentation
----------------------

ReST syntax
___________

ReST syntax is text based as markdown or wiki language.

Install *sphinx*::

    virtualenv sphinx
    source sphinx/bin/activate
    pip install -r requirements.txt

Edit the targeted source file from ``source/rst/``::

    vim source/rst/api.rst

Follow sphinx documentation `online`_.

.. _online: http://www.sphinx-doc.org/en/stable/contents.html


Generate new doc locally::

    make html

Generate Epub::

    make html epub

You can read the generated doc from ``build/html/index.html``.
