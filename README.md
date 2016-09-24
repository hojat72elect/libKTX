# KTX

**K**o**t**lin utilities for LibGD**X** applications.

### About the project

If you want to follow the JVM path, [LibGDX](http://libgdx.badlogicgames.com/) is arguably the best framework to create
games out there: it targets most important platforms, has ton of extensions, is pretty fast and allows you to go low-level,
as well as hide all the shaders and OpenGL stuff behind pleasant abstractions. It certainly has its issues and some
questionable design choices, but it seems that [people](https://github.com/SquidPony/SquidLib) would still rather
[base](https://github.com/oakes/play-clj) their [stuff](https://mini2dx.org/) on LibGDX rather than write new frameworks
from scratch. Considering how much work it takes to prepare a game framework/engine, it is only understandable.

The two biggest issues with LibGDX are the facts that some of its modules were clearly not designed to be extended
(*raise a hand if you never copy-pasted a `Scene2D` actor in sheer frustration, as a simple class extension was not enough!*)
and that it is written in *Java*. Do not get me wrong: Java 8 was a huge step forward, but since you likely want to support
legacy Android devices and WebGL (through GWT), you're stuck with Java 6 or 7. Switching to Kotlin - with its extension
functions, inline methods, builders, operator overriding, pleasant syntax, easier generics and whatnot - certainly helps.
But since LibGDX was not designed with Kotlin in mind, there's still *a lot of work* to be done to make use of all the
shiny new features. *A lot of work* that has to be done *once*, if you think about it.

**KTX** aims to make LibGDX Kotlin-friendly, without turning the API upside down. This is **not** a new framework by any
means.

### Modules

Needless to say, you might not want or need all the features provided by **KTX**. That is why it was designed to be highly
modular from day one: some of its libraries are just a single Kotlin file. When possible, the extensions do not include
the standard Kotlin library, and even if they do - it is marked as a `provided` dependency, so you can choose the Kotlin
version that suits you best (since Kotlin is already pretty stable, this should not cause any issues as long as you use
a recent release).

The modules present in **KTX** are:

- [actors](actors): general `Scene2D` utilities for stages, actors, actions and event listeners.
- [assets](assets): assets and heavy resources management utilities.
- [collections](collections): utilities for LibGDX custom collections. Based on Kotlin standard library utilities.
- [i18n](i18n): some simple functions that make internationalization less verbose and easier to use.
- [inject](inject): unsettlingly simple dependency injection with nearly zero runtime overhead.
- [log](log): minimal runtime overhead cross-platform logging.
- [math](math): operator overloads for LibGDX math API and general math utilities.
- [scene2d](scene2d): type-safe Kotlin builders for Scene2D GUI. *(Not yet implemented.)*
- [style](style): enhances `Skin` API with type-safe builders of official Scene2D widget styles.
- [vis](vis): type-safe Kotlin builders for VisUI. Alternative to the [scene2d](scene2d) extension.
- [vis-style](vis-style): enhances `Skin` API with type-safe builders of VisUI widget styles. Extension of [style](style) module.

Afraid to use some third-party code? Run the test suites yourself. *Every* function and class added by these extensions
features in at least one unit test.

### Gradle

The project itself is managed by [Gradle](http://gradle.org/). Gradle wrapper is not included, so you might want to
install it locally. If you consider working from sources, these are some useful Gradle tasks that you can look into:

- `gradle build install` - builds the libraries' archives and pushes them to Maven Local.
- `gradle test` - runs unit tests in all projects.
- `gradle clean` - removes build directories.
- `gradle distZip` - prepares a zip archive with all jars in `build/distributions` folder. Useful for releases.
- `gradle uploadArchives` - pushes the archives to Maven Central. Requires proper `gradle.properties` with signing and
logging data.
- `gradle closeAndPromoteRepository` - closes and promotes Nexus repository. Should be run after `uploadArchives` in
case of a non-snapshot upload to Maven Central.

### Contribution

Want to help? Great. Browse through issues (if any) to see what's currently missing or broken. Before creating any pull
requests, be aware that the code is dedicated to public domain.

