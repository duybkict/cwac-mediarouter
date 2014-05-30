CWAC-MediaRouter: Going Where Google Declined To Go, For Some Reason...
======================================================

This project offers a port of `MediaRouteActionProvider`, and its support
classes, to work with
native API Level 11+ fragments and the action bar. These were ported
from the `mediarouter` Android library project, where these classes
require the `appcompat` action bar and, hence, the fragment backport.

The sincere hope is that Google will ship an equivalent to this someday, at
which point in time this library will be deprecated.

Installation
------------
This Android library project is 
[available as a JAR](https://gihub.com/commonsguy/cwac-mediarouter/releases).

This project is also available as
an artifact for use with Gradle. To use that, add the following
blocks to your `build.gradle` file:

```groovy
repositories {
    maven {
        url "https://repo.commonsware.com.s3.amazonaws.com"
    }
}

dependencies {
    compile 'com.commonsware.cwac:mediarouter:0.1.+'
}
```

Or, if you cannot use SSL, use `http://repo.commonsware.com` for the repository
URL.

If you elect to clone this repo, or download a ZIP of this repo, and use it
as a source-based library project, you will need to add your own copy of the
`android-support-v4.jar` to your copy of `libs/` in the library project, as it
is not supplied.

Usage: MediaRouteActionProvider
-------------------------------
You use this the same as you would use the official `mediarouter` edition, with
the following changes:

- Use `Activity` instead of `ActionBarActivity`.

- Use the native API Level 11 version of fragments, rather than the Android Support
package's backport.

- You do not need (or want) a theme based on `Theme.AppCompat`, but rather can use
ordinary themes (e.g., `Theme.Holo.Light.DarkActionBar`).

- Your menu resources and such will need to reference
`com.commonsware.cwac.mediarouter.MediaRouteActionProvider` rather than
`android.support.v7.app.MediaRouteActionProvider`. Menu resources should also
use the regular `android:actionProviderClass` attribute for specifying this class,
rather than the alternative required by `appcompat` (e.g., `app:actionProviderClass`).

- Your import for `MediaRouteActionProvider` will need to change to the aforementioned
class. Most other `android.support.v7` imports will remain as-is, particularly
`MediaRouter` itself. If you are using an IDE that supports bulk import resolution
(e.g., Eclipse with Ctrl-Shift-O), you might consider deleting all `android.support.v7`
imports and let the IDE help you grab the `com.commonsware.cwac.mediarouter` ones
where needed.

Dependencies
------------
This project depends upon the `mediarouter` library project, because it still
references classes from there, particularly `MediaRouter` itself. That, in turn,
will require `appcompat`. However, your *code* will not need to use `appcompat`,
and ProGuard should strip a lot of the junk out.

The minimum supported SDK for this library is API Level 14. If you want to support
older devices, you should be using `appcompat` and the fragments backport anyway.

Version
-------
This is version v0.1.1 of this module, meaning it is a wee bit more than a proof
of concept, but not by all that much.

Demo
----
There are two sample projects, `demo/` and `demo-remoteplayback/`, that illustrate
the use of this library. The first one just shows the `MediaRouteActionProvider` and
shows you the route when it changes. The second one demonstrates the currently-flaky
`RemotePlaybackClient` class, for playing back media on a device like a Chromecast.

License
-------
The code in this project is licensed under the Apache
Software License 2.0, per the terms of the included LICENSE
file. Most of the library's code is licensed this way by Google; the changes
made to that code to implement the port are licensed this way by CommonsWare.

Questions
---------
If you have questions regarding the use of this code, please post a question
on [StackOverflow](http://stackoverflow.com/questions/ask) tagged with `commonsware` and `android`. Be sure to indicate
what CWAC module you are having issues with, and be sure to include source code 
and stack traces if you are encountering crashes.

If you have encountered what is clearly a bug, or if you have a feature request,
please post an [issue](https://github.com/commonsguy/cwac-mediarouter/issues).
Be certain to include complete steps for reproducing the issue.

Do not ask for help via Twitter.

Also, if you plan on hacking
on the code with an eye for contributing something back,
please open an issue that we can use for discussing
implementation details. Just lobbing a pull request over
the fence may work, but it may not.

Release Notes
-------------
- v0.1.1: removed `android-support-v4.jar` from `libs/` to improve Gradle compatibility
- v0.1.0: initial release

Who Made This?
--------------
<a href="http://commonsware.com">![CommonsWare](http://commonsware.com/images/logo.png)</a>

