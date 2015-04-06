# Mac OS X XAR Extensions #

A few Mac OS X Extensions have been written to integrate xar into the
Mac OS X environment.  This document details them, and gives some technical
information on debugging them if you run into problems.

## Spotlight Plugin ##

The Spotlight plugin is under subversion in the xarmdimport directory.
It can be build by simply executing 'xcodebuild' from within that directory,
and will create a build/Release/xar.mdimporter bundle.  Double clicking on
this bundle, or typing 'open build/Release/xar.mdimporter' will bring
up a dialog box asking if you want to install it, and it'll install into
/Library/Spotlight.

To debug why the plugin isn't working, there are two commands most useful:
  * First, verify that LaunchServices is picking up the xar file mapping.
This can be done with: "/System/Library/Frameworks/CoreServices.framework/Frameworks/LaunchServices.framework/Support/lsregister -dump" and you should see something that looks like this:
```
        type    id:            16444
                uti:           xar.xar
                description:   xar!
                flags:         exported  active  apple-internal  
                icon:          
                delegate:      Spotlight/xar.mdimporter/
                conforms to:   public.data, public.content
                tags:          .xar
```
  * Second, try importing the file manually with debug info on using the command: mdimport -d 2 /path/to/foo.xar" and you should see something like this:
```
    kMDItemContentType = "xar.xar";
    kMDItemContentTypeTree =     (
        "xar.xar",
        "public.data",
        "public.item",
        "public.content"
    );
    kMDItemCreator = xar;
    kMDItemDisplayName =     {
        "" = "bin.xar";
    };
    kMDItemKind = "XAR!";
    kMDItemTextContent = " bin bin/[ bin/bash bin/cat bin/chmod bin/cp bin/csh b
in/date bin/dd bin/df bin/domainname bin/echo bin/ed bin/expr bin/hostname bin/k
ill bin/ksh bin/launchctl bin/link bin/ln bin/ls bin/mkdir bin/mv bin/pax bin/ps
 bin/pwd bin/rcp bin/rm bin/rmdir bin/sh bin/sleep bin/stty bin/sync bin/tcsh bin/test bin/unlink bin/wait4path bin/zsh bin/zsh-4.3.4";
}
(Info) Import: Import '/Users/bbraun/bin.xar' type 'xar.xar' using '/Library/Spo
tlight/xar.mdimporter'
```

## Quick Look Plugin ##
For those running 10.5 and later, there is a Quick Look plugin in subversion
under 'xarql'.  It can be built simply using the command 'xcodebuild' within
that directory and will generate a 'build/Release/xar.qlgenerator' bundle.
Install this file by dragging it with the finder to ~/Library/QuickLook.
It takes a few seconds for the system to pick up the new bundle and update
the LaunchServices database, and you're supposed to log out and log back
in again before Quick Look plugins are picked up.  However, you can avoid
the login/logout if you use 'qlmanage -r' to tell quicklookd to pick up the
new plugin.  If all works properly, you should have something more exciting
than the default blank icon for .xar files.

If something isn't going properly, here are some hints to debug it:
  * As with the Spotlight plugin, the first thing to do is verify that
LaunchServices is picking up the xar file mapping.
This can be done with: "/System/Library/Frameworks/CoreServices.framework/Frameworks/LaunchServices.framework/Support/lsregister -dump" and you should see something that looks like this:
```
type            id:            17056
                uti:           xar.xar
                description:   XARchive
                flags:         imported  inactive  apple-internal  
                icon:          
                delegate:      QuickLook/xar.qlgenerator/
                conforms to:   public.archive
                tags:          .xar
```
  * Second, if the mapping is correct, use 'qlmanage -t /path/to/foo.xar'
to manually attempt to get a thumbnail rendered.  'qlmanage -m' will
give you some additional information about what plugins are registered
and for what UTI Types.