Fork of `pyBarcode <https://bitbucket.org/whitie/python-barcode/>`_
project.

This library provides a simple way to create barcodes using only the
Python standardlib. The barcodes where created as SVG objects.


Requirements
------------

    - Setuptools/distribute for installation (new in version 0.7beta4)
    - Python 2.6 or above (including Python 3.x)
    - On Python 2.6, 3.0, 3.1: argparse (for the commandline script)
    - Program to open SVG objects (your browser should do it)
    - Optional: PIL to render barcodes as images (PNG, JPG, ...)


Installation
------------

Make sure you have setuptools/distribute installed.

Unpack the downloaded file, cd into the viivakoodi directory and run
`python setup.py install`. Or just copy the barcode dir somewhere in
your PYTHONPATH.

The best way is to use pip: `pip install viivakoodi`.


Provided Barcodes
-----------------

EAN-8, EAN-13, EAN-14, UPC-A, JAN, ISBN-10, ISBN-13, ISSN, Code 39, Code 128, PZN


Todo
----

    - Add documentation
    - Improve Python 3 support

Usage
-----

Interactive::

    >>> import barcode
    >>> barcode.PROVIDED_BARCODES
    [u'code39', u'code128', u'ean', u'ean13', u'ean8', u'gs1', u'gtin',
     u'isbn', u'isbn10', u'isbn13', u'issn', u'jan', u'pzn', u'upc', u'upca']
    >>> EAN = barcode.get_barcode_class('ean13')
    >>> EAN
    <class 'barcode.ean.EuropeanArticleNumber13'>
    >>> ean = EAN(u'5901234123457')
    >>> ean
    <barcode.ean.EuropeanArticleNumber13 object at 0x00BE98F0>
    >>> fullname = ean.save('ean13_barcode')
    >>> fullname
    u'ean13_barcode.svg'
    # Example with PNG
    >>> from barcode.writer import ImageWriter
    >>> ean = EAN(u'5901234123457', writer=ImageWriter())
    >>> fullname = ean.save('ean13_barcode')
    u'ean13_barcode.png'
    # New in v0.4.2
    >>> from io import BytesIO
    >>> fp = BytesIO()
    >>> ean.write(fp)
    # or
    >>> f = open('/my/new/file', 'wb')
    >>> ean.write(f) # PIL (ImageWriter) produces RAW format here
    # New in v0.5.0
    >>> from barcode import generate
    >>> name = generate('EAN13', u'5901234123457', output='barcode_svg')
    >>> name
    u'barcode_svg.svg'
    # with file like object
    >>> fp = StringIO()
    >>> generate('EAN13', u'5901234123457', writer=ImageWriter(), output=fp)
    >>>

Now open ean13_barcode.[svg|png] in a graphic app or simply in your browser
and see the created barcode. That's it.

Commandline::

    $ pybarcode{2,3} create "My Text" outfile
    New barcode saved as outfile.svg.
    $ pybarcode{2,3} create -t png "My Text" outfile
    New barcode saved as outfile.png.

    Try `pybarcode -h` for help.

Changelog
---------

:v0.1: First release.

