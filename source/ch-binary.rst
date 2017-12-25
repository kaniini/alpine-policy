Binary packages and indices
===========================

Alpine uses the ``apk-tools`` package manager and therefore deals with ``.apk`` package
files and ``APKINDEX.tar.gz`` index files.  Both file types follow the same basic
structure.


.. s-binary-structure:

Binary file structure
---------------------

Alpine binary package and index files are distributed as two distinct tarballs that have
been combined into a single gzip stream.  These are the ``control`` and ``data`` tarballs.


.. s-binary-control:

``control`` tarball
~~~~~~~~~~~~~~~~~~~

The ``control`` tarball is the first tarball appearing in a valid ``apk-tools`` binary file.
It contains a number of control files depending on the type of binary file, but *must*
contain a signature file which is a signature of the ``data`` tarball.

File entries stored in the ``control`` tarball *must* be prefixed with a period (``.``).


.. s-binary-data-signature:

The ``.SIGN.RSA.*`` file
++++++++++++++++++++++++

Files beginning with ``.SIGN.RSA`` are considered to be signatures on the data section of
the binary file.  Files are usually suffixed with the filename of the public key which signed
them, but the package manager *must* check the signature against all installed trusted keys.

The signature is a signed SHA1 digest of the data tarball, which is verified using any installed
key.  The use of ``RSA`` in the signature file name is for historical reasons and has no relation
to what keys will be checked.  Other mechanisms, such as ECDSA are supported, but not used in the
official Alpine repositories, but will still retain the ``.SIGN.RSA`` filename prefix.


The ``.SIGN.DSA.*`` file
++++++++++++++++++++++++

This is a historic signature file format and should only be encountered when processing very old
packages and is based on a broken implementation of the DSA signature scheme.  It *must not* ever
be used in new packages.


.. s-binary-data:

``data`` tarball
~~~~~~~~~~~~~~~~

The ``data`` tarball is the second tarball appearing in a valid ``apk-tools`` binary file.
It contains either the filesystem provided by a package, or the actual index data, depending on
the type of binary file being parsed.


.. s-binary-index:

Index files
-----------

Repository index files provide an index of the packages present in a repository, and their versions.
The package index filename *must* be ``APKINDEX.tar.gz``.

The ``control`` section *must* only include a signature file.

The ``data`` section contains two files:

``APKINDEX``
  The package index itself.

``DESCRIPTION``
  A human-readable name for the repository as a one-line text file.


.. s-binary-index-apkindex:

The ``APKINDEX`` file
~~~~~~~~~~~~~~~~~~~~~

The ``APKINDEX`` file contains an index of all packages stored in the repository.  It consists of a
series of stanzas that include multiple control fields, which represent package index entries.  Stanzas
are separated by newlines.  A typical stanza looks like:

::

    C:Q124zpd1DU3ZeHbcB6Ufb8BW/wSTk=
    P:busybox
    V:1.27.2-r2
    A:x86_64
    S:488986
    I:921600
    T:Size optimized toolbox of many common UNIX utilities
    U:http://busybox.net
    L:GPL2
    o:busybox
    m:Natanael Copa <ncopa@alpinelinux.org>
    t:1508479039
    c:610a62d3321f856f62d5271ae558d5cf1e3ae986
    D:so:libc.musl-x86_64.so.1
    p:/bin/sh command:busybox command:sh

.. s-binary-index-apkindex-fields:

``APKINDEX`` control fields
+++++++++++++++++++++++++++

``C``
  A raw SHA1 checksum of the package stored in base64 encoding.

``P``
  The name of the package.

``V``
  The version of the package.

``A``
  The architecture of the package.

``S``
  The size of the package file in octets.

``I``
  The installed size of the package.

``T``
  A one-line description of the package.

``U``
  The URL of the package's website.

``L``
  The license of the package.

``o``
  The source package name (in Alpine this would be the ``APKBUILD`` name).

``m``
  The maintainer of the package.

``t``
  The timestamp when the package was signed.

``c``
  The GIT commit hash if available.

``D``
  The dependencies of the package.

``p``
  A list of dependencies that this package may provide.

``i``
  Any install-if rules that would trigger automatic installation of this package.


.. s-binary-package:

Binary packages
---------------

Binary packages contain the distributed software that is part of the Alpine
distribution.  Binary packages must meet appropriate criteria for inclusion in
the Alpine package repositories.


.. s-binary-package-files:

Binary package files
~~~~~~~~~~~~~~~~~~~~

Binary package files are processed by ``apk-tools`` when it installs new packages,
and are referred to by repository index files.

The control archive includes a ``.PKGINFO`` file as well as several optional
maintainer scripts.


.. s-binary-package-pkginfo:

``.PKGINFO`` file format
++++++++++++++++++++++++

The ``.PKGINFO`` file contains general metadata about the binary package, such as
the *origin aport*, *commit* and *maintainer* in a key-value format.

The format used is described by these rules:

* ``#`` is used for comments
* a declaration consists of the form: ``key``, followed by whitespace and ``=``, followed by ``value``.


.. s-binary-package-pkginfo-fields:

``.PKGINFO`` file fields
++++++++++++++++++++++++

``pkgname``
  The name of the binary package.

``pkgver``
  The version of the binary package.

``pkgdesc``
  The description of the binary package.

``url``
  The URL for the upstream website concerning the binary package.

``builddate``
  The UNIX timestamp when the package was built.

``packager``
  The name and email of the user who built the binary package.  See ``$PACKAGER`` in ``abuild.conf``.

``size``
  The size of the binary package when extracted to disk in octets.

``arch``
  The architecture of the binary package.

``origin``
  The origin aport which generated this binary package.

``commit``
  The GIT commit hash which this binary package was generated from.

``replaces_priority``
  The replaces priority, a numeric value which is used by ``apk-tools`` to determine which package should
  have final ownership of a file.  Higher values have higher priority.

``provider_priority``
  The provider priority, a numeric value which is used by ``apk-tools`` to break ties when choosing a
  virtual package to satisfy a dependency.  Higher values have higher priority.

``provides``
  Designates that the package provides a given dependency.  Providers that are unversioned are considered
  virtual.

``depend``
  Designates that the package has a given dependency.

``install_if``
  Designates that the package should be installed if the declared ``install_if`` dependencies are present.

``license``
  The license of the binary package.  Should be provided as an SPDX_-compliant license name.

``triggers``
  Path patterns to register the ``.trigger`` maintainer script against.

``datahash``
  The SHA2-256 checksum of the data archive.

.. _SPDX: https://spdx.org/licenses/


.. s-binary-package-maintainer-scripts:

Binary package maintainer scripts
+++++++++++++++++++++++++++++++++

Binary packages can contain several maintainer scripts, these are:

``.trigger``
  Trigger scripts are run when a path entry is modified that matches one or more of the path patterns
  registered to the package, such as when another package adds a file to ``/bin``, for example.

``.pre-install``
  A script run before installation of the package.

``.post-install``
  A script run after installation of the package.

``.pre-deinstall``
  A script run before deinstallation of the package.

``.post-deinstall``
  A script run after deinstallation of the package.

``.pre-upgrade``
  A script run before upgrade of the package.

``.post-upgrade``
  A script run after upgrade of the package.


.. s-binary-package-naming-rules:

Binary package naming rules
+++++++++++++++++++++++++++

Binary package names must only contain alphanumeric characters, dashes or periods.


.. s-binary-package-version-rules:

Binary package versioning rules
+++++++++++++++++++++++++++++++

Binary package versions consist of one or more numbers separated by a period.  The final
number may have a single letter following it (``1.1g``), but should not be used to indicate
pre-release status -- the ``apk`` package manager considers ``1.1b`` to be newer than
``1.1``.

A suffix can be provided to denote pre-release or patch status:

========== ========================
  Suffix   Meaning
========== ========================
``_alpha`` Alpha release (earliest)
``_beta``  Beta release
``_pre``   Pre release
``_rc``    Release candidate
(none)     Normal release
``_p``     Patch release
========== ========================

Any of these suffixes may be followed by a number.

The last component of the version is the Alpine package revision, in the form ``-r0``.  The first
package version for a given upstream release must always end in ``-r0``.
