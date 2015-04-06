# API Documentation #
## xar\_t xar\_open(const char **file, int32\_t flags) ##**

Obtain a handle to an existing or new xarchive

### Description ###

xar\_open() returns a handle to an in memory representation of a xarchive. The first argument, file, is the relative or absolute path to the xarchive that is to be opened/created. The second argument, flags can be one of either READ, which will open the xarchive read only (useful for extracting from the xarchive or listing the contents), or WRITE which will create a new xarchive.

When a xarchive is opened with READ, the binary and xml headers are both parsed prior to the return of xar\_open(). xar\_open() allocates a handle and other state information which must be free'd by calling xar\_close() on the returned xar\_t handle.

On success, a valid handle is returned. On failure, NULL is returned.

### Example ###

```
#include <xar/xar.h>

int main(int argc, char *argv[]) {
	xar_t x;

	x = xar_open(argv[1], READ);
	if( x == NULL ) {
		fprintf(stderr, "Error opening xarchive: %s\n", argv[1]);
		exit(1);
	}

	...

	xar_close(x);
	
	...

}
```