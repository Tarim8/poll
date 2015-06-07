NAME
====

  __poll__ ---- monitor special files, character devices and named pipes for changes.


SYNOPSIS
========

  __poll__ [ [_OPTIONS_] _FILE_ ]...


DESCRIPTION
===========

  __poll__ outputs a special file's contents, when it changes, one line at a time.
  It is intended for use with files such as GPIO inputs which appear in the /sys file system.
  It will also work with named pipes and character devices but not normal files.
  It is often of use with embedded Linux machines such as the Raspberry Pi.

  __poll__, contrary to what its name suggests, sleeps between changes in files.
  It is based on the system library __poll__(2).

  Examples:

    poll --debounce 20 --unique "+gpio %l %t\n" /sys/class/gpio/gpio4/value --default --delimiter '\2\3\r\n' "+rfid %l\n" /dev/ttyAMA0

  Monitor a switch conected to a GPIO pin and an RFID reader connected to a serial port.
  Output the switch value and a time (in nanoseconds) when it changes state ignoring any bouncing for 20ms after it is switched.
  Output the value read by the RFID reader, delimited by any of ctrl-B, ctrl-C, carriage return and newline.


OPTIONS
=======

  Options apply to all subsequent files until they are overridden.

##      _+FORMAT_

  Controls output.  Interpretted sequences are:

    %l  Line from file
    %p  Filename
    %t  Time since Unix epoch in nanoseconds
    %%  A single %

##      __--debounce__ _TIME_

  After a value change, wait this amount of time (in milliseconds) before reporting any further change.
  Useful with __--unique__ as switch bouncing will be completely ignored.

##      __--unique__

  Only report unique values.
  Useful with __--debounce__.

##      __--duplicates__

  Allow all values to be output (opposite of __--unique__).

##      __--delimiters__ _STRING_

  Lines in the file are delimited by one of the characters in _STRING_.

##      __--default__

  Set options back to default values.


CAVEATS
=======
  Hard coded to have a limit of 64 files and an input line length of 1024 characters.
  Won't list changes to a "normal" file - use __tail -f__ instead.

AUTHOR
======
  Written by Tarim.
  Errors to <poll-cmd@mediaplaygrounds.co.uk>.

SEE ALSO
========
  __poll__(2), __tail__(1)
