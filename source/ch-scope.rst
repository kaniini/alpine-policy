About this manual
=================

.. _s1.1:

Scope
-----

This manual describes the current policy requirements for the Alpine Linux
distribution.  This includes the structure and contents of the Alpine Linux
repositories, technical discussions of how various distribution components
function, and technical requirements that packages must meet for inclusion
in Alpine Linux releases.

This manual also describes the current policy as it relates to making
packages for Alpine.  It is however, not a tutorial on how to create packages,
nor is it an exhaustive technical specification for low-level components.

In such cases where an expanded technical discussion of a specific topic is
helpful, we have included footnotes, but the contents discussed in footnotes
should be considered non-normative.  Additionally, any appendices are not
necessarily normative either, but we have tried to clarify if an appendix
should be considered normative or not.

In the normative sections of this manual, the words *must*, *should*, and
*may*, and the adjectives *required*, *recommended* and *optional*, are used
to distinguish the significance of various guidelines discussed in this
manual.  Packages that do not conform to the guidelines denoted by *must* or
*required* will generally not be considered acceptable for the Alpine
distribution.  Non-conformance with guidelines denoted by *should* or
*recommended* will generally be considered a bug, but will not necessarily
render a package unsuitable for inclusion in the distribution.  Guidelines
denoted by *may* or *optional* are truly optional and adherence is left to
the maintainer's discretion.  [#]_

Much of the information in this manual will likely be useful even when
building packages for local use only.

.. _s1.2:

New versions of this document
-----------------------------

This manual is distributed via the Alpine package
`alpine-policy <https://pkgs.alpinelinux.org/package/edge/main/x86/alpine-policy>`_.

TODO: figure out how to include the policy manual on the website


.. [#]
   This is similar to RFC 2119.  However, it should be noted that this
   document uses those words differently.
