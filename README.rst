ERequests: Asyncronous Requests
===============================

ERequests allows you to use Requests with Eventlet to make asyncronous HTTP
Requests easily.

ERequests is a port to Eventlet of Kenneth Reitz's grequests (https://github.com/kennethreitz/grequests)

Usage
-----

Usage is simple::

    import erequests

    urls = [
        'http://httpbin.org/delay/3',
        'http://www.heroku.com',
        'http://tablib.org',
        'http://python-requests.org',
        'http://kennethreitz.com'
    ]

Create a set of unsent Requests::

    >>> rs = (erequests.get(u) for u in urls)

Send them all at the same time::

    >>> erequests.map(rs)
    [<Response [200]>, <Response [200]>, <Response [200]>, <Response [200]>, <Response [200]>]

Exception handling::

    >>> def exception_handler(request):
    >>>     return '%s' % request.exception
    >>> rs = (erequests.get(u, timeout=1, exception_handler=exception_handler) for u in urls)
    >>> erequests.map(rs)
    ["HTTPConnectionPool(host='httpbin.org', port=80): Request timed out. (timeout=1)", <Response [200]>, <Response [200]>, <Response [200]>, <Response [200]>]

In case of exception the exception_handler is called with the request as argument. The actual exception is found in `request.exception`.

Installation
------------

Installation is easy with pip::

    $ pip install erequests

