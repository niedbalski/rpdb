rpdb - remote debugger based on pdb
==================================

rpbm is a wrapper around pdb that re-routes stdin and stdout to a socket
handler. By default it opens the debugger on port 4444::

    import rpdb; rpdb.set_trace()

But you can change that by simply instantiating Rpdb manually::

    import rpdb
    debugger = rpdb.Rpdb(12345)
    debugger.set_trace()

It is known to work on Jython 2.5 to 2.7, Python 2.5 to 3.1. It was written
originally for Jython since this is pretty much the only way to debug it when
running it on Tomcat.

Upon reaching `set_trace()`, your script will "hang" and the only way to get it
to continue is to access rpdb using telnet, netcat, etc..::

    nc 127.0.0.1 4444

Installation on CPython (standard Python)
-----------------------------------------

    pip install rpdb

Installation in a Tomcat webapp
-------------------------------

Just copy the rpdb directory (the one with the __init__.py file) in your
WEB-INF/lib/Lib folder along with the standard Jython library (required).

Known bugs
----------
  - The socket is not always closed properly so you will need to ^C in netcat
    and ^\ in telnet to exit after a continue.
  - There is a bug in Jython 2.5/pdb that causes rpdb to stop on ghost
    breakpoints after you continue ('c'), this is fixed in 2.7b1.

Author(s)
---------
Bertrand Janin <b@janin.com> - http://tamentis.com/

This is inspired by:

    http://bugs.python.org/issue721464
    http://snippets.dzone.com/posts/show/7248
