# CWAC-MediaRouter: Going Where Google Declined To Go, For Some Reason...

This project offers a port of the `mediarouter-v7` Android
library project, to work with
native API Level 11+ fragments and the action bar. While `mediarouter-v7`
requires you to use `appcompat-v7` and the fragments backport,
this project eliminates those requirements.

Note that this library was substantially extended in version 0.2.0 to
be a complete cross-port of `mediarouter-v7`. Formerly, it only contained
`MediaRouteActionProvider` and a few related support classes.

## Installation

This project is available as
an artifact for use with Gradle. To use that, add the following
blocks to your `build.gradle` file:

```groovy
repositories {
    maven {
        url "https://repo.commonsware.com.s3.amazonaws.com"
    }
}

dependencies {
    compile 'com.commonsware.cwac:mediarouter:0.2.+'
}
```

Or, if you cannot use SSL, use `http://repo.commonsware.com` for the repository
URL.

Eclipse users will need to clone this repository, import the `mediarouter/` project
into the Eclipse workspace, then attach that project as an Android library project
to the app (Project > Properties > Android).

If you elect to clone this repo, or download a ZIP of this repo, and use it
as a source-based library project, you will need to add your own copy of the
`android-support-v13.jar` to your copy of `libs/` in the library project, as it
is not supplied.

## Usage

Basically, everywhere you see `android.support.v7.app` or
`android.support.v7.media` classes from `mediarouter-v7`, replace them
with `com.commonsware.cwac.mediarouter.app` and
`com.commonsware.cwac.mediarouter.media` equivalents.
And, of course, rather than using `appcompat-v7` and `ActionBarActivity`,
or using the fragments backport, you would use the native action bar
and native fragments implementations.

Note that your menu resources and such will need to reference
`com.commonsware.cwac.mediarouter.app.MediaRouteActionProvider` rather than
`android.support.v7.app.MediaRouteActionProvider`. Menu resources should also
use the regular `android:actionProviderClass` attribute for specifying this class,
rather than the alternative required by `appcompat` (e.g., `app:actionProviderClass`).

## Upgrading From 0.1.x to 0.2.0

If you were using the 0.1.x implementation of this library, please note
that:

- You will need to change your class references, in menu resources
and imports. Formerly, you would have used `com.commonsware.cwac.mediarouter`
as the package for classes like `MediaRouteActionProvider`. Those classes
all moved into the `com.commonsware.cwac.mediarouter.app` package, to
better match the rest of `mediarouter-v7`.

- You should remove your dependency on `mediarouter-v7`.

## Dependencies

This project depends upon `support-v13` and `support-annotations` from
the Android Support Pacakge. It does **not** depend upon `mediarouter-v7`
or `appcompat-v7`.

The minimum supported SDK for this library is API Level 14. If you want to support
older devices, you should be using `appcompat-v7` and the fragments backport anyway.

## Version

This is version v0.2.0 of this module, meaning it is a wee bit more than a proof
of concept, but not by all that much.

## Demo

There are two sample projects, `demo/` and `demo-remoteplayback/`, that illustrate
the use of this library. The first one just shows the `MediaRouteActionProvider` and
shows you the route when it changes. The second one demonstrates the currently-flaky
`RemotePlaybackClient` class, for playing back media on a device like a Chromecast.

## License

The code in this project is licensed under the Apache
Software License 2.0, per the terms of the included LICENSE
file. Most of the library's code is licensed this way by Google; the changes
made to that code to implement the port are licensed this way by CommonsWare.

## Questions

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

## Release Notes

- v0.2.0: overhaul to eliminate `mediarouter-v7` dependency
- v0.1.4: updated for Android Studio 1.0 and new AAR publishing system
- v0.1.3: removed unused resources
- v0.1.2: added `cwac-` JAR prefix, updated Gradle for Android plugin and dependencies, tightened up manifest
- v0.1.1: removed `android-support-v4.jar` from `libs/` to improve Gradle compatibility
- v0.1.0: initial release

##Who Made This?

<a href="https://commonsware.com">![CommonsWare](http://commonsware.com/images/logo.png)</a>

