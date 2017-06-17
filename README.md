# Introduction

`cleanbyage` is a tool that removes files based on atime, oldest first, until
there is enough space/inodes free.

It is commonly used to ensure that tmp/scratch and cache file systems
have space available.

File systems are traversed only if the start clean limit is triggered.
Cleanup is then done until the stop clean limit is reached, which allows
tuning for fewer file system traversals by doing more cleanup each time.

There is support for specifying a regexp of files to always be preserved.

# Installation

Requires perl and a few common modules, see the script for details.

# Usage

`cleanbyage /path/to/directory/to/clean`

To see all options, do:

`cleanbyage -h`

# Hints

Cleaning is done by looking at the time of last access, atime, returned
by `stat()`.

Obviously this won't work if you have disabled atime by using the noatime
mount option.

On Linux, ensure that atime gets updated often enough to be relevant. The
`relatime` default mount option updates only every 24 hours. If more accuracy
is required we recommend using the `lazytime` or, if not available,
`strictatime` mount option.
