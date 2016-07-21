..
.. NB:  This file is machine generated, DO NOT EDIT!
..
.. Edit vmod.vcc and run make instead
..

.. role:: ref(emphasis)

.. _vmod_header(3):

===========
vmod_header
===========

-----------------------
Header VMOD for Varnish
-----------------------

:Manual section: 3

SYNOPSIS
========

import header [from "path"] ;

DESCRIPTION
===========

Varnish Module (vmod) for manipulation of duplicated HTTP headers, for instance
multiple Set-Cookie headers.

CONTENTS
========

* :ref:`func_append`
* :ref:`func_copy`
* :ref:`func_get`
* :ref:`func_remove`

.. _func_append:

VOID append(HEADER, STRING_LIST)
--------------------------------

Prototype
	VOID append(HEADER, STRING_LIST)

Description
        Append an extra occurrence to an existing header.
Example
	::

		header.append(beresp.http.Set-Cookie, "foo=bar")

.. _func_copy:

VOID copy(HEADER, HEADER)
-------------------------

Prototype
	VOID copy(HEADER, HEADER)

Description
        Copy all source headers to a new header.
Example
	::

		header.copy(beresp.http.set-cookie, beresp.http.x-old-cookie);

.. _func_get:

STRING get(PRIV_CALL, HEADER, STRING)
-------------------------------------

Prototype
	STRING get(PRIV_CALL, HEADER header, STRING regex)

Description
        Fetches the value of the first `header` that matches the given
        regular expression `regex`.
Example
	::

		set beresp.http.xusr = header.get(beresp.http.set-cookie,"user=");

.. _func_remove:

VOID remove(PRIV_CALL, HEADER, STRING)
--------------------------------------

Prototype
	VOID remove(PRIV_CALL, HEADER header, STRING regex)

Description
        Remove all occurences of `header` that matches `regex`.
Example
	::

	        header.remove(beresp.http.set-cookie,"^(?!(funcookie=))");



ACKNOWLEDGEMENTS
================

The development of this plugin was made possible by the sponsorship of
Softonic, http://en.softonic.com/ .

Also thanks to Imo Klabun and Anders Nordby for bug reports.

BUGS
====

You can't use dynamic regular expressions, which also holds true for normal
regular expressions in regsub().
