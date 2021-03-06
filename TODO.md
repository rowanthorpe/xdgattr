TODO
====

* for v0.2:
    * add BASH completion file
    * improve ZSH completion file:
        * File-completion for starting-with-colon syntax could list files relative to xdgattr $base_dir (but
          retain the leading ":")
        * Value-completion for "remove tags" could be a function to complete a comma-separated list of
          existing tags/comments in the file using:
            *  "_multi_parts , [array-of-tags-and-taglists]"?,
            *  "_sequence ..."?,
            *  "_values -s , ..."?

* for v0.3:
    * add more field_types from xdg specs, see:
        * https://www.freedesktop.org/wiki/CommonExtendedAttributes/#proposedmetadataattributes
        * https://www.freedesktop.org/wiki/CommonExtendedAttributes/#relationtodublincore

* for ~v0.9:
    * adding $KSH_VERSION to the 'set -o posix' test works for pdksh but kills ksh - find how to distinguish between those two shells

* for ~v1.5:
    * add handling for FreeBSD equivalent xattrs:
        * https://www.freebsd.org/cgi/man.cgi?query=getextattr
    * add handling for MacOS-X equivalent xattrs:
        * https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/xattr.1.html
    * add handling for OS/2, Windoze (NTFS, HPFS) equivalent xattrs:
        * https://blogs.msdn.microsoft.com/wsl/2016/06/15/wsl-file-system-support/
    * add handling for OS/2, Windoze (FAT) equivalent xattrs:
        * http://www.tavi.co.uk/os2pages/eadata.html
    * add handling for Solaris equivalent xattrs:
        * https://docs.oracle.com/cd/E26505_01/html/816-5175/fsattr-5.html
    * add handling for AIX equivalent xattrs:
        * http://www.ibm.com/support/knowledgecenter/en/ssw_aix_71/com.ibm.aix.cmds2/getea.htm
