# heroku-deps-build-pack

A Heroku build pack for Clojure using tools.deps

Create a `Procfile` in the root of your project to define which alias(es) will be used at startup

```
web: clojure -A:my-alias-list
```

Please read the [standard Heroku docs](https://devcenter.heroku.com/articles/preparing-a-codebase-for-heroku-deployment) for preparing apps.

### JVM runtime [Optional]

Heroku uses JDK 8 by default.
 
Here is [a link to the very specific the Heroku Java support doc](https://devcenter.heroku.com/articles/java-support#supported-java-versions) for how this can be changed
