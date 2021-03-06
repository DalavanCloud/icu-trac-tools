ICU Code Tools plugin

© 2016 and later: Unicode, Inc. and others.
License & terms of use: http://www.unicode.org/copyright.html

Copyright (C) 2010-2014 IBM Corporation and Others. All Rights Reserved.
See license.html for the license file. This file is part of the
ICU project and is under the same license.

Docs:  https://sites.google.com/site/icucodetools/home

Requirements:
	Trac 0.12+
	Repository

Installing:
	1. install the plugin - at least the ticketmanager and review portion.

         a. There is no source release at this time: I recommend
             that you check out this code with svn
             and in this directory, run:
                "python setup.py develop"

	 b. In trac.ini under '[components]' add:
		icucodetools.review.reviewmodule = enabled
		icucodetools.ticketmgr.ticketmanager = enabled

	NOTE: DCUT and TKTLIST parts are not working yet.
	Don't bother to enable them.

	2. in your trac.ini describe how your changesets describe a ticket.
	Our changesets look like this:  "ticket:1234: fixed the broken code"
	We use this regex:

	   [icucodetools]
	   ticket_pattern = ^ticket:(\d+)

	3. you may need to run trac-admin <environment> upgrade

	4. Grant permission of ICUREVIEW_VIEW to whomever you want to
	   be able to review tickets.

	5. Now, any ticket will have something in the top right corner which says:
	     "No commits" - no commits against this ticket

	     "Review 1 commits"  - there is only one commit. Clicking this link
	             will just take you to that single changeset.

	      "Review n commits"  - there are more than one commits against this
	             ticket.


Troubleshooting:

Q: My commits aren't being found!
A: Check the debug log. It will note commits with unparseable messages

Q: How do I resync the commits?
A: Until we implement trac 0.12 changeset listeners, you can do this:

    0.  back up your path/to/env/db/trac.db

    1. $ sqlite3  path/to/env/db/trac.db

    2. sqlite> delete from rev2ticket;

    3. sqlite> update system set value='-1' where name='icu_tktmgr_youngest';

    4. sqlite>  .quit

Now the ticket manager will re-sync the first time you hit a ticket.

RESTRICT CHECKINS
 See the comments at the top of icucodetools/traccheck.py.
 note that /path/to/traccheck is the path to the installed "traccheck" script,
 not the 'traccheck.py' source file.

FILING BUGS/FEATURE REQUESTS:
 - See https://sites.google.com/site/icucodetools/home to file or view bugs.

LICENSE:
 - see LICENSE

