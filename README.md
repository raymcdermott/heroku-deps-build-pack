# heroku-deps-build-pack : deploy without uberjars

A Heroku build pack for Clojure using tools.deps with some special tricks to speed up deployment without uberjars.

Why not uberjars?
1) it's extra work and operational activities that need to be created, maintained and could go wrong
2) after you get it working, are you 100% sure that the CLASSPATH with an uberjar is the same as it is without it?
3) did you test against the uberjar or the unpacked code?
4) we have a LISP, don't do this to yourself
6) And no it doesn't need Docker

On that last point, the Heroku way is kind of like Docker: it builds your program and creates an image for deployment. This buildpack is a way to provide that image with all the needed Clojure tools. Now with some extra tricks cos we know Heroku and we know Clojure.

The tricks enable you to use the build phase to compile your ClojureScript and pull in all the dependencies for your server.

## Heroku primer

Please read the [standard Heroku docs](https://devcenter.heroku.com/articles/preparing-a-codebase-for-heroku-deployment) for preparing apps.

Create a `Procfile` in the root of your project to define which alias(es) will be used at startup

```
web: clojure -A:my-alias-list
```

### Build Aliases [Optional]

You may specify one or more aliases to run during the `compile` phase of the deployment using a [config var](https://devcenter.heroku.com/articles/config-vars#managing-config-vars)

:information_source: This is how you can compile your ClojureScript app and make sure its always fresh.

```
heroku config:set BUILD_ALIASES=":alias1:alias2"
```

### Test Aliases [Optional]

You may specify one or more aliases to run during the `compile` phase of the deployment using a [config var](https://devcenter.heroku.com/articles/config-vars#managing-config-vars)

:information_source: This is how you can ensure that your server dependencies are on your CLASSPATH and don't need to be downloaded again when you try to start the server.

One simple test that triggers the server dependency is all that is needed here. No biggieif you have more tests.

```
heroku config:set TEST_ALIASES=":alias1:alias2"
```

:information_source: Main win: any artefacts built or dependencies downloaded during the `compile` phase will be available at deployment.

### JVM runtime [Optional]

Heroku uses JDK 8 by default.
 
Here is [a link to the very specific the Heroku Java support doc](https://devcenter.heroku.com/articles/java-support#supported-java-versions) for how this can be changed
