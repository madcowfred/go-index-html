
index-html
==========

A simple Go HTTP server to replace lighttpd's default file browser and downloader interface with additional features.

Features
---

 * Adds custom sort ability via two methods
   * Create a dummy file named `.index-sort-**sort-method**` in the directory to sort
   * Supply `?sort=**sort-method**` query-string parameter in request (overrides dummy file)
   * Folders are always sorted to display before files
   * Available sorting methods:
     * `name-asc`  sorts by file name in ascending order (default)
     * `name-desc` sorts by file name in descending order
     * `date-asc`  sorts by last modified time in ascending order
     * `date-desc` sorts by last modified time in descending order
 * 302 redirect support for relative symlinks
   * Requests for symlinks will 302 redirect to the target file (or folder) if that target is
     found within the filesystem root jail.

Arguments
---

  `./index-html <web root> <filesystem root> <listen address>`

Starts a Go HTTP server listening at `<listen address>` expecting HTTP proxy requests for paths
starting with `<web root>`, serving requests for directory listings and/or file downloads for
filesystem objects found under `<filesystem root>`.

chroot is not used to provide the filesystem root jail due to cross-platform compatibility concerns.