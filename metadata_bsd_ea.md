# BSD Extended Attributes #

FreeBSD-style Extended Attributes. The [Wikipedia ACLs entry on FreeBSD ACLs](http://en.wikipedia.org/wiki/Extended_file_attributes#FreeBSD) has a good overview.

## Implementation status ##

Implemented.

## Notes ##

  * Attempting to read the system namespace while not a privileged user is expected to return an error. The system namespace is used, among other things, for storing kernel extended attributes such as ACLs.