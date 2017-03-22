xdgattr
=======

A tool for editing freedesktop.org (xdg) extended attributes of files.

Intended to portably wrap extended attribute implementations on many platforms,
but in this early incarnation it only wraps `getfattr`/`setfattr` as found on
most GNU/Linux platforms. Obviously requires the filesystem to handle xattrs
and to be mounted with the appropriate option. Beware that on most platforms if
you `mv`/`cp`/`tar` the files to a non-xattr-capable filesystem/archive the
xattrs will be silently dropped.

Quick Start
-----------

* Copy xdgattr to somewhere in your `$PATH`
* Install auto-complete files to the appropriate location for your shell if you
  want (once they've been created - TODO)
* Run `xdgattr --help` for details
* For integration with `recoll` copy the info from the /recoll subdirectory to
  the appropriate places

License
-------

Copyright © 2017 Rowan Thorpe <rowan@rowanthorpe.com>

xdgattr uses the GPLv3 license, check the COPYING file.

Rationale
---------

Having had to make many hurried backups and quick migrations over the
years/decades (due to moving house, failing hard-drives, etc) I never had time
to find old files, so I ended up with several external drives (Terabytes) full
of backed up files - many of them duplicated across multiple archives because I
hadn't had time to filter already backed-up files. In the end because I
couldn't find files I mostly gave up trying/remembering - which is as bad as
having just deleted it all. When I finally got some time to do something about
it (namely condense, deduplicate and index it) the scope of the problem was
overwhelming mostly because there was so much historical "TODO" content
spanning so many unrelated subjects that it was pointless trying to construct a
useful tree hierachy (which just turned one opaque forest into another opaque
forest). Just making it all searchable was not useful either because:

* I would have had to create an internal mini-Google to index that much data,
  and I don't have those kind of resources or time to spare.
* Real-time searching rather than indexing would have been so painfully slow,
  redundant and heavy-duty that it would have just created more failing
  hard-drives before long, and turned me off trying to find/rescue data, or
  both.
* It would have required me to know what to search for, but I primarily needed
  to rescue stuff that had been on long-term freeze for so long I'd forgotten
  it was there, or what it was, and there was so much I would forget again what
  searches are useful before long anyway.

The solution I needed was a tagging system which is:

* Closely coupled to (preferably a part of) the filesystem, to avoid the
  nightmare stories that can be found online where the database in someone's
  custom tagging system got corrupted or deleted, when external tools moved
  files out from under the daemon, when the software got deprecated, etc.
* Quickly and easily browsable and searchable from a simple desktop tool, so I
  can get fast visual overviews rather than constructing lengthy commandlines
  and parsing verbose output every time I want to find something.
* Quickly and easily browsable and searchable from the commandline when
  appropriate so I am not bound to GUIs when I want to do complicated searches.
* Not bound to a specific desktop daemon - or any desktop (I want to access
  stuff from a virtual terminal or over ssh too).
* Quick and simple to add/update/remove tags from the commandline so I can
  bulk-tag when appropriate to speed up the initial tagging process.

I found [recoll](https://en.wikipedia.org/wiki/Recoll) a good match for
desktop-independent visual browser/searcher, it includes recollq for
commandline searching, and it can update search-indexes by cron or realtime
(inotify). Most importantly it can index extended attributes as "fields" for
search and display (see the included config-fragments/diffs included in the
"recoll" directory for integration help).

Having found an indexing/browsing/searching-by-tag solution, I needed a tool
for creating/updating/deleting tags. [pxattr](http://www.lesbonscomptes.com/pxattr)
seems to overlap with this but would have required me hacking on top of it in
C++ even if it turned out to be relevant enough. I chose for now to just create
a portable-shellscript wrapper around the system xattr commandline utils, for
the sake of quick prototyping, ease of porting and ease of installation. Later
on I will migrate it to a more performant and robust language/bindings.

Personally, I use it for tagging files only within a specific directory
(pointed to by the $xdgattr_dir var, which can be edited in the script or
overridden by environment-variable), accessing all files there using the
":/dir/dir/file" syntax, and only allowing recoll to index that directory - and
of course ensuring that directory is on a xattr-enabled filesystem.
