# API Documentation #
## Overview ##
Below are some brief descriptions of the programming interface to xar, and some examples of how to use it.

xar\_t [xar\_open](API_xar_open.md)(const char **file, int32\_t flags);**

void [xar\_close](API_xar_close.md)(xar\_t x);

xar\_file\_t [xar\_add](API_xar_add.md)(xar\_t x, const char **path);**

xar\_file\_t [xar\_add\_frombuffer](API_xar_add_frombuffer.md)(xar\_t x, xar\_file\_t parent, const char **name, char**buffer, size\_t length);

xar\_file\_t [xar\_add\_folder](API_xar_add_folder.md)(xar\_t x, xar\_file\_t f, const char **name, struct stat**info);

int32\_t [xar\_extract](API_xar_extract.md)(xar\_t x, xar\_file\_t f);

void [xar\_register\_errhandler](API_xar_register_errhandler.md)(xar\_t x, err\_handler callback, void **usrctx);**

xar\_file\_t [xar\_err\_get\_file](API_xar_err_get_file.md)(xar\_errctx\_t ctx);

const char **[xar\_err\_get\_string](API_xar_err_get_string.md)(xar\_errctx\_t ctx);**

int [xar\_err\_get\_errno](API_xar_err_get_errno.md)(xar\_errctx\_t ctx);

xar\_iter\_t [xar\_iter\_new](API_xar_iter_new.md)();

void [xar\_iter\_free](API_xar_iter_free.md)(xar\_iter\_t i);

xar\_file\_t [xar\_file\_first](API_xar_file_first.md)(xar\_t x, xar\_iter\_t i);

xar\_file\_t [xar\_file\_next](API_xar_file_next.md)(xar\_iter\_t i);

int32\_t [xar\_opt\_set](API_xar_opt_set.md)(xar\_t x, const char **option, const char**value)

const char **[xar\_opt\_get](API_xar_opt_get.md)(xar\_t x, const char**option

int32\_t [xar\_prop\_set](API_xar_prop_set.md)(xar\_file\_t, const char **key, const char**value)

int32\_t [xar\_prop\_get](API_xar_prop_get.md)(xar\_file\_t, const char **key, const char****value)**

const char **[xar\_prop\_first](API_xar_prop_first.md)(xar\_file\_t f, xar\_iter\_t i)**

const char **[xar\_prop\_next](API_xar_prop_next.md)(xar\_iter\_t i)**

int32\_t [xar\_attr\_set](API_xar_attr_set.md)(xar\_file\_t f, const char **property, const char**key, const char **value)**

const char **[xar\_attr\_get](API_xar_attr_get.md)(xar\_file\_t f, const char** property, const char **key)**

const char **[xar\_attr\_first](API_xar_attr_first.md)(xar\_file\_t f, const char**prop, xar\_iter\_t i)

const char **[xar\_attr\_next](API_xar_attr_next.md)(xar\_iter\_t i)**


xar\_subdoc\_t [xar\_subdoc\_new](API_xar_subdoc_new.md)(xar\_t x, const char **name)**

int32\_t [xar\_subdoc\_prop\_set](API_xar_subdoc_prop_set.md)(xar\_subdoc\_t s, const char **key, const char**value)

int32\_t [xar\_subdoc\_prop\_get](API_xar_subdoc_prop_get.md)(xar\_subdoc\_t s, const char **key, const char****value)**

xar\_subdoc\_t [xar\_subdoc\_first](API_xar_subdoc_first.md)(xar\_t x)

xar\_subdoc\_t [xar\_subdoc\_next](API_xar_subdoc_next.md)(xar\_subdoc\_t s)

const char **[xar\_subdoc\_name](API_xar_subdoc_name.md)(xar\_subdoc\_t s)**

int32\_t [xar\_subdoc\_copyout](API_xar_subdoc_copyout.md)(xar\_subdoc\_t s, unsigned char buf, unsigned int **size)**

int32\_t [xar\_subdoc\_copyin](API_xar_subdoc_copyin.md)(xar\_subdoc\_t s, unsigned char **buf, unsigned int size)**

void [xar\_subdoc\_remove](API_xar_subdoc_remove.md)(xar\_subdoc\_t s)