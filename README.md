# heroku-deps-build-pack

A Heroku build pack for Clojure using tools.deps

Please read the [standard Heroku docs](https://devcenter.heroku.com/articles/preparing-a-codebase-for-heroku-deployment) for preparing apps.

Create a `Procfile` in the root of your project to define which alias(es) will be used at startup

```
web: clojure -A:my-alias-list
```

### Build Aliases [Optional]

You may specify one or more aliases to run during the `compile` phase of the deployment using a [config var](https://devcenter.heroku.com/articles/config-vars#managing-config-vars)

```
heroku config:set BUILD_ALIASES=":alias1:alias2"
```

### Build Aliases [Optional]

You may specify one or more aliases to run during the `compile` phase of the deployment using a [config var](https://devcenter.heroku.com/articles/config-vars#managing-config-vars)

```
heroku config:set TEST_ALIASES=":alias1:alias2"
```

:information_source: Any dependencies downloaded during the `compile` phase will be cached.

### JVM runtime [Optional]

Heroku uses JDK 8 by default.
 
Here is [a link to the very specific the Heroku Java support doc](https://devcenter.heroku.com/articles/java-support#supported-java-versions) for how this can be changed
