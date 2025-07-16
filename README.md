PlusDataStore
===============

This project organizes PlusToolkit sample/test data, publicly available SDKs, etc.

To support content-based addressing, files are uploaded as assets organized in [releases](https://github.com/PlusToolkit/PlusLibData/releases)
named after the hashing algorithm.

For each hashing algorithm `<HASHALGO>` (MD5, SHA256, ...), you will find:
* release named `<HASHALGO>`
* a CSV file `<HASHALGO>.csv` listing all `<hashsum>;<filename>` pairs
* markdown document `<HASHALGO>.md` with links of the form `* [<filename>](https://github.com/PlusToolkit/PlusLibData/releases/download/<HASHALGO>/<checksum>)` (this file is regenerated on each upload from the CSV file, therefore files should be renamed or deleted by editing the CSV file)

_The commands reported below should be evaluated in the same terminal session. See [Documentation conventions](#documentation-conventions)_

Upload files
------------

1. Install [Prerequisites](#prerequisites)

2. Copy files to upload in `INCOMING` directory.

3. Run process_release_data.py script specifying your github token and upload command.

```
$ python process_release_data.py upload --github-token 123123...123
```

4. Optional: Clear content of `INCOMING` directory if all files have been uploaded for each `<HASHALGO>`.

Download files
--------------

1. Install [Prerequisites](#prerequisites)

2. Run process_release_data.py script specifying your github token, download command, and hash algorithm. If multiple versions of the same filename are available then the unique file names will be generated in the download folder by attaching the checksum to the end of each original filename.

```
$ python process_release_data.py download --github-token 123123...123
```

Rename a file
-------------

Download `<HASHALGO>.csv` file from the corresponding release, edit it, upload the modified version, and run `process_release_data upload`.

Note: Since each file is identified by hash sum, changing the filename does not affect the ability to find and download files. Filenames are only stored in the repository to allow generation of user-friendly file names.

Delete a file
-------------

Download `<HASHALGO>.csv` file from the corresponding release, remove the line referring to the file that should be deleted, upload the modified version, and run `process_release_data upload`. Remove the referred file from the release assets.

Note: Deleting files should be avoided (even if an old version of a file is replaced by a new one), because tests in earlier software versions may still expect to find previously uploaded files. Deleting is only recommended for immediate removal files that have just been uploaded by mistake.

Prerequisites
-------------

1. Download this project

```
$ git clone git://github.com/PlusToolkit/PlusLibData
```

2. Install Python and [githubrelease](https://github.com/j0057/github-release#installing) package

```
$ pip install githubrelease
```

3. [Create a github personal access token](https://help.github.com/articles/creating-an-access-token-for-command-line-use) with "repo" scope to get read/write access to the repository


Documentation conventions
-------------------------

Commands to evaluate starts with a dollar sign. For example:

```
$ echo "Hello"
Hello
```

means that `echo "Hello"` should be copied and evaluated in the terminal.

History
-------

This is based on the method used in the [SlicerDataStore](https://github.com/Slicer/SlicerDataStore).
