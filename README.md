Zimbra ZCO Report Script
========================

Overview
--------

Report the versions of the Zimbra Connector for Outlook currently in use
based on the Zimbra mailbox.log file(s).

This script will report a space separated list of login date, name and
address, the ZCO versioni, and the most recent date this version wasi
used and where this entry can be found in the log file.

All versions should also be reported as "[unauthorized]" due to the fact
that the username won't be available until after the user was logged in
(use fgrep if you want to skip these lines).

It accepts an optional first parameter to specify the location of the
log file(s).

Please be patient when running this script.


Examples
--------

* Don't report the pre-authenticated versions:

        zmzcoreport | fgrep -v '[unauthenticated]'

* Suppress the IP address due to privacy concerns:

        zmzcoreport | cut -d' ' -f1-3,5

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



Example Output
--------------

    $ zmzcoreport | fgrep -v '[unauthenticated]' | my-magic-obfuscator
    user01@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:58124
    user02@example.com 7.2.1.547 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:58121
    user03@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:34838
    user04@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:43882
    user05@example.com 7.2.2.579 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:37106
    user06@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:46638
    user07@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:33026
    user08@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:58219
    user09@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:58135
    user10@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:34010
    user11@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:57899
    user12@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:58210
    user13@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:58212
    user14@example.com 7.2.2.579 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:10907
    user15@example.com 7.2.2.579 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:58200
    user15@example.com 7.2.3.677 20130605 192.0.2.102 /opt/zimbra/log/mailbox.log.2013-06-05.gz:62368
    user16@example.com 7.2.2.579 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:55610
    user17@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:58141
    user18@example.com 7.2.2.579 20130605 192.0.2.102 /opt/zimbra/log/mailbox.log.2013-06-05.gz:7850
    user18@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:33006
    user19@example.com 7.2.1.547 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:9286
    user20@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:58202
    user21@example.com 7.2.2.579 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:58132
    user22@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:35669
    user23@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:36318
    user24@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:48393
    user25@example.com 7.2.2.579 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:58193
    user26@example.com 7.2.3.677 20130606 192.0.2.102 /opt/zimbra/log/mailbox.log:58199



Known Bugs
----------

* Sometimes the last line of a log files causes a warning like

        Use of uninitialized value in split at zmzcoreport line 77, <$fh> line 272246.

  Which is the reconversion of the date.  Might be caused by gunzip not
  behaving or a missing line break.



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

