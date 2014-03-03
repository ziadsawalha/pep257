PEP 257 docstring style checker
===========================================================

**pep257** is a static analysis tool for checking
compliance with Python `PEP 257
<http://www.python.org/dev/peps/pep-0257/>`_.

The framework for checking docstring style is flexible, and
custom checks can be easily added, for example to cover
NumPy `docstring conventions
<https://github.com/numpy/numpy/blob/master/doc/HOWTO_DOCUMENT.rst.txt>`_.

Installation
-----------------------------------------------------------

Use `pip <http://pip-installer.org>`_ or easy_install::

    pip install pep257

Alternatively, you can use ``pep257.py`` source file
directly--it is self-contained.

**pep257** is tested with Python 2.6, 2.7, 3.2, 3.3

Example
-----------------------------------------------------------

.. code::

    $ pep257 --help
    Usage: pep257 [options] [<file|dir>...]

    Options:
      --version             show program's version number and exit
      -h, --help            show this help message and exit
      -e, --explain         show explanation of each error
      -s, --source          show source for each error
      --ignore=<codes>      ignore a list comma-separated error codes, for
                            example: --ignore=D101,D202
      --match=<pattern>     check only files that exactly match <pattern> regular
                            expression; default is --match='(?!test_).*\.py' which
                            matches files that don't start with 'test_' but end
                            with '.py'
      --match-dir=<pattern>
                            search only dirs that exactly match <pattern> regular
                            expression; default is --match-dir='[^\.].*', which
                            matches all dirs that don't start with a dot

    $ pep257 test.py
    test.py:18 in private nested class `meta`:
            D101: Docstring missing
    test.py:22 in public method `method`:
            D102: Docstring missing
    ...

    $ pep257 test.py --explain
    test.py:18 in private nested class `meta`:
            D101: Docstring missing

            All modules should normally have docstrings.  [...] all functions and
            classes exported by a module should also have docstrings. Public
            methods (including the __init__ constructor) should also have
            docstrings.

            Note: Public (exported) definitions are either those with names listed
                  in __all__ variable (if present), or those that do not start
                  with a single underscore.
    ...

    $ pep257 test.py --source
    test.py:15 in public class `class_`:
            D101: Docstring missing

        15: class class_:
        16:
    ...

Error codes
-----------------------------------------------------------

All **pep257** errors have unique codes. All codes start with a capital D and
are grouped as follows:

+--------------+--------------------------------------------------------------+
| **Missing docstrings**                                                      |
+--------------+--------------------------------------------------------------+
| D10{0,1,2,3} | Public {module,class,method,function} missing.               |
+--------------+--------------------------------------------------------------+
| **Whitespace issues**                                                       |
+--------------+--------------------------------------------------------------+
| D200         | One-line docstrings should fit on one line with quotes.      |
+--------------+--------------------------------------------------------------+
| D20{1,2}     | No blank lines allowed {before,after} docstring.             |
+--------------+--------------------------------------------------------------+
| D20{3,4}     | 1 blank required {before,after} class docstring.             |
+--------------+--------------------------------------------------------------+
| D205         | Blank line required between one-line summary and description.|
+--------------+--------------------------------------------------------------+
| D206         | Docstring should be indented with spaces, not tabs.          |
+--------------+--------------------------------------------------------------+
| D20{7,8}     | Docstring {under,over}-indented.                             |
+--------------+--------------------------------------------------------------+
| **Quotes issues**                                                           |
+--------------+--------------------------------------------------------------+
| D300         | Use """triple double quotes""".                              |
+--------------+--------------------------------------------------------------+
| D301         | Use r""" if any backslashes in your docstring.               |
+--------------+--------------------------------------------------------------+
| D302         | Use u""" for Unicode docstrings (Python 2 only).             |
+--------------+--------------------------------------------------------------+
| **Docstring content issues**                                                |
+--------------+--------------------------------------------------------------+
| D400         | First line should end with a period.                         |
+--------------+--------------------------------------------------------------+
| D401         | First line should be in imperative mood.                     |
+--------------+--------------------------------------------------------------+
| D402         | First line should not be the function's "signature".         |
+--------------+--------------------------------------------------------------+
| **Deprecated checks (see PEP-257)**                                         |
+--------------+--------------------------------------------------------------+
| D209         | Multi-line docstring should end with 1 blank line.           |
+--------------+--------------------------------------------------------------+
