=============
freegeoip.net
=============
:Info: See `github <http://github.com/fiorix/freegeoip>`_ for the latest source.
:Author: Alexandre Fiori <fiorix@gmail.com>

About
=====

This is the software running behind the IP Geolocation Web Service at `freegeoip.net <http://freegeoip.net>`_.
The database is not shipped with the package. However, there are instructions for downloading and generating a local version of the database, using the ``database/createdb.py`` python script.

Using
-----

The web service can deliver search results in three different formats: CSV, XML and JSON (with callbacks).

- For querying GeoIP information (using curl)::

    curl http://freegeoip.net/csv/google.com
    curl http://freegeoip.net/xml/69.63.189.16
    curl http://freegeoip.net/json/74.200.247.59
    curl http://freegeoip.net/json/github.com?callback=doit

- For querying GeoIP information about your own IP::

    curl http://freegeoip.net/xml/

- For querying Timezone information (/tz/``country_code``/``region_code``)::

    curl http://freegeoip.net/tz/xml/BR/27
    curl http://freegeoip.net/tz/json/US/10
    curl http://freegeoip.net/tz/json/CA/10?callback=doit


Running
=======

For development::

    export PYTHONPATH=`pwd`
    twistd -n freegeoip

For production, check out the ``scripts`` directory. There are init scripts for debian - single instance, or multiple instances for multi-core systems. I recommend load balancing with Nginx.

Depends on `redis <http://redis.io>`_.


Requirements
------------

- `cyclone <http://github.com/fiorix/cyclone/>`_
- `Python <http://python.org/>`_ 2.5 or newer (but not 3.x)
- `SQLite3 <http://www.sqlite.org/>`_ (usually ships with Python)
- `Twisted <http://twistedmatrix.com/trac/>`_ 8.2 or newer

From the Command Line
---------------------

I usually use the following in ~/.bash_profile or ~/.bashrc in order to easily query the geoip database from the Unix command line::

    # geoip
    function geoip_curl_xml { curl -D - http://freegeoip.net/xml/$1 }
    alias geoip=geoip_curl_xml

Testing
-------
Check out scripts/test.py.


Credits
=======

Thanks to (in no particular order):

- google.com

    - Because it wouldn't look so good without the map

- twitter.com

    - Bootstrap makes dirty programmers feel like artists

- ipinfodb.com

    - For formely providing both GeoIP and Timezones database

- maxmind.com

    - For creating the database
