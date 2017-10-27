Distributions and Repositories
==============================

The Alpine Linux operating system is maintained as a series of *distributions* containing
groups of *packages*.  Since there are many packages, they are split into several
*repositories* in order to make handling them easier.


.. s-licensing-guidelines:

Alpine Software Licensing Guidelines
------------------------------------

The Alpine Software Licensing Guidelines are used to determine whether a package's license
is acceptable for inclusion in the repositories.  They are based on the OSI Open Source
definition.

The guidelines are:

1. Free Redistribution
    The license shall not restrict any party from selling or giving away the software as a
    component of an aggregate software distribution containing programs from several different
    sources.  The license shall not require a royalty or other fee for such sale.

2. Source Code
    The program must include source code, and must allow distribution in source code as well as
    binary form.

3. Derived Works
    The license must allow modifications and derived works, and must allow them to be distributed
    under the same terms as the license of the original software.

4. Integrity of The Author's Source Code
    The license may restrict source-code from being distributed in modified form *only* if the
    license allows the distribution of "patch files" with the source code for the purpose of
    modifying the program at build time.  The license must explicitly permit distribution of
    software built from modified source code.  The license may require derived works to carry a
    different name or version number from the original software.

5. No Discrimination Against Persons or Groups
    The license must not discriminate against any person or group of persons.

6. No Discrimination Against Fields of Endeavor
    The license must not restrict anyone from making use of the program in a specific field
    of endeavor.  For example, it may not restrict the program from being used in a business,
    or from being used for genetic research.

7. Distribution of License
    The rights attached to the program must apply to all to whom the program is redistributed
    without the need for execution of an additional license by those parties.

8. License Must Not Be Specific to a Product
    The rights attached to the program must not depend on the program's being part of a particular
    software distribution. If the program is extracted from that distribution and used or
    distributed within the terms of the program's license, all parties to whom the program is
    redistributed should have the same rights as those that are granted in conjunction with
    the original software distribution.

9. License Must Not Restrict Other Software
    The license must not place restrictions on other software that is distributed along with the
    licensed software. For example, the license must not insist that all other programs distributed
    on the same medium must be open-source software.

10. License Must Be Technology-Neutral
     No provision of the license may be predicated on any individual technology or style of interface.

11. Example Licenses
     The "GPL," "BSD," "MIT," and "ISC" licenses are examples of licenses that would be considered
     acceptable.


.. s-repos:

Repositories
------------

Each distribution consists of multiple repositories.  A repository is a directory of ``.apk``
files and an index called ``APKINDEX.tar.gz``.

The ``.apk`` binary format is discussed in the binary packages chapter, and the APKINDEX format
is discussed in an appendix.


.. s-repo-main:

The ``main`` repository
~~~~~~~~~~~~~~~~~~~~~~~

Packages considered essential to the core Alpine system are included in the ``main`` repository.

Packages included in ``main`` have final QA responsibility belonging to the core team, instead of
the maintainer, which allows for a 2 year maintenance lifecycle.  Primary maintenance reponsibility
is left with the maintainer.

The ``main`` repository is the only repository enabled by default.


.. s-repo-community:

The ``community`` repository
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Packages maintained by the greater Alpine community are located in the ``community`` repository.

All maintenance reponsibility, except in rare circumstances, is left with the maintainer.  Packages
in the ``community`` repository have a 6 month maintenance lifecycle.

Package changes which have not received any feedback within a reasonable time may be accepted
without an approval from the maintainer as long as those changes are policy compliant.


.. s-repo-testing:

The ``testing`` repository
~~~~~~~~~~~~~~~~~~~~~~~~~~

Packages which are work in progress are located in the ``testing`` repository.  There is no maintenance
reponsibility, and broken packages are usually disabled.

The ``testing`` repository is not included in any released distribution, and is only available in Alpine
``edge`` which is an unreleased distribution.
