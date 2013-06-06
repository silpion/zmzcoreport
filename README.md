Zimbra ZCO Report Script
========================

Overview
--------

Report the versions of the Zimbra Connector for Outlook currently in use
based on the Zimbra mailbox.log file(s).

This script will report a space separated list of login name, version
and the most recent date this version was used.  All users should also
be reported as "[unauthorized]" due to the fact that the username won't
be available until after the user was logged in (use fgrep if you want
to skip these lines).

It accepts an optional first parameter to specify the location of the
log file(s).

Please be patient when running this script.


Examples
--------

* Don't report the pre-authenticated versions:

        zmzcoreport | fgrep -v '[unauthenticated]'

* Sort by version, oldest first:

        zmzcoreport | sort -k 2 -V 

* Sort by last login date, most recent first:

        zmzcoreport | sort -k 3 -n -r

* Read sort(1) for more examples:

        zmzcoreport | sort -k 2,2V -k 3,3nr -k 1,1

* You probably don't want to do this:

        curl https://raw.github.com/silpion/zmzcoreport/master/zmzcoreport | perl

* You probably don't want to to do this either:

        zmzcoreport /var/lib/vz/private/opt/zimbra/log


License
-------

Copyright (c) 2013, Silpion IT-Solutions GmbH <http://www.silpion.de>
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met: 

* Redistributions of source code must retain the above copyright notice, this
  list of conditions and the following disclaimer. 
* Redistributions in binary form must reproduce the above copyright notice,
  this list of conditions and the following disclaimer in the documentation
  and/or other materials provided with the distribution. 

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR
ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

