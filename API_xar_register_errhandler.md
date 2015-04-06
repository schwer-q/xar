# API Documentation #

## void xar\_register\_errhandler(xar\_t x, err\_handler callback, void **usrctx) ##**

typedef int32\_t (**err\_handler)(int32\_t severit, int32\_t instance, xar\_errctx\_t ctx, void**usrctx);

Register a callback to handle messages from libxar

### Description ###

libxar uses a callback function to inform the calling application about any warnings or errors that occur. The callback will be passed back as much relevant information as possible, including a reference to the xar\_file\_t that experienced the problem (if any), an error string, and any relevant errno value in addition to any caller supplied context information.

xar\_register\_errhandler() is the callback registration routine. The first parameter, x is the handle of the open xarchive the callback is to be associated with, the second parameter is the callback function, and the third parameter is a reference to caller supplied context information.
The user supplied context information will be passed to the callback function as the last argument, usrctx.
The callback function may obtain xar related context information via the following accessor functions (using the callback function's third argument, ctx):

xar\_file\_t xar\_err\_get\_file(xar\_errctx\_t ctx);
const char **xar\_err\_get\_string(xar\_errctx\_t ctx);
int xar\_err\_get\_errno(xar\_errctx\_t ctx);**

### Example ###
```
#include <xar/xar.h>

static int32_t err_callback(int32_t sev, int32_t err, xar_errctx_t ctx, void *usrctx) {
	xar_file_t f;
	const char *str;
	int e;

	f = xar_err_get_file(ctx);
	str = xar_err_get_string(ctx);
	e = xar_err_get_errno(ctx);

	switch(sev) {
	case XAR_SEVERITY_DEBUG:
	case XAR_SEVERITY_INFO:
		break;
	case XAR_SEVERITY_WARNING:
	case XAR_SEVERITY_NORMAL:
		printf("%s\n", str);
		break;
	case XAR_SEVERITY_NONFATAL:
	case XAR_SEVERITY_FATAL:
		printf("Error while ");
		if( err == XAR_ERR_ARCHIVE_CREATION ) printf("creating");
		if( err == XAR_ERR_ARCHIVE_EXTRACTION ) printf("extracting");
		printf(" archive\n");
		if( str ) printf(": %s", str);
		if( err ) printf(" (%s)", strerror(e));
		if( sev == XAR_SEVERITY_NONFATAL ) printf(" - ignored");
		printf("\n");
		break;
	}
	return 0;
}

int main(int argc, char *argv[]) {
	xar_t x;

	x = xar_open(argv[1], WRITE);
	if( x == NULL ) {
		fprintf(stderr, "Error opening xarchive: %s\n", argv[1]);
		exit(1);
	}

	xar_register_errhandler(x, err_callback, NULL);

	if( xar_add(x, "/path/to/file") == NULL ) {
		fprintf(stderr, "Error adding /path/to/file to the xarchive\n");
	}

	...

	xar_close(x);
	
	...

}

```