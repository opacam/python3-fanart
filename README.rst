=======================================
Python3 interface to fanart.tv API (v3)
=======================================

.. image:: https://api.travis-ci.org/opacam/python3-fanart.png?branch=master
   :target: http://travis-ci.org/opacam/python3-fanart

.. image:: https://coveralls.io/repos/github/opacam/python3-fanart/badge.svg?branch=master
   :target: https://coveralls.io/github/opacam/python3-fanart?branch=master

    
.. image:: https://pypip.in/v/python3-fanart/badge.png
   :target: https://pypi.python.org/pypi/python3-fanart

.. image:: https://pypip.in/d/python3-fanart/badge.png
   :target: https://pypi.python.org/pypi/python3-fanart

This package provides a module to interface with the `fanart.tv`_. It's a fork
of the project named `python-fanart`_ but updated to work with
`fanart.tv api v3`. It also limits the python version to 3.4+, because the end
of life of python2 it's near (2020). To use this package you need your own
**api key**. You can request your api key in here: `fanart.tv api key`_


.. contents::
    :local:

.. _installation:

Installation
============
Using pip::

    $ pip install git+https://github.com/opacam/python3-fanart

.. _summary:

FANART API Summary
==================

Low Level
---------

::

    from fanart.core import Request
    import fanart
    request = Request(
        apikey='<YOURAPIKEY>',
        id='24e1b53c-3085-4581-8472-0b0088d2508c',
        ws=fanart.WS.MUSIC,
        type=fanart.TYPE.ALL,
        sort=fanart.SORT.POPULAR,
        limit=fanart.LIMIT.ALL,
    )
    print(request.response())


Music
-----

::

    import os
    os.environ.setdefault('FANART_APIKEY', '<YOURAPIKEY>')
    import requests

    from fanart.music import Artist

    artist = Artist.get(id='24e1b53c-3085-4581-8472-0b0088d2508c')
    print(artist.name)
    print(artist.mbid)
    for album in artist.albums:
        for cover in album.covers:
            print('Saving: %s' % cover)
            _, ext = os.path.splitext(cover.url)
            filepath = os.path.join(path, '%d%s' % (cover.id, ext))
            with open(filepath, 'wb') as fp:
                fp.write(cover.content())

Movie
-----

::

    import os
    os.environ.setdefault('FANART_APIKEY', '<YOURAPIKEY>')

    from fanart.movie import Movie

    movie = Movie.get(id='70160')


TV Shows
--------

::

    import os
    os.environ.setdefault('FANART_APIKEY', '<YOURAPIKEY>')

    from fanart.tv import TvShow

    tvshow = TvShow.get(id='80379')

.. _license:

License
=======

This software is licensed under the ``Apache License 2.0``. See the ``LICENSE``
file in the top distribution directory for the full license text.

.. _references:

References
==========
* `fanart.tv`_
* `python-fanart`_
* `fanart.tv api key`_

.. _fanart.tv: http://fanart.tv/
.. _python-fanart: https://github.com/z4r/python-fanart
.. _fanart.tv api key: https://fanart.tv/get-an-api-key/
