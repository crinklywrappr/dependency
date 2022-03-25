[![Clojars Project](https://img.shields.io/clojars/v/com.github.crinklywrappr/dependency.svg)](https://clojars.org/com.github.crinklywrappr/dependency)

Stuart Sierra's dependency library, but I started over using `deps-new` to get a feel for the new deps thing.

# Manual steps required (or things which could be in a template)

1. `deps-new` generates a `pom.xml` but this appears to be worthless - just delete it
2. `bb/jar` generates a POM which is missing a lot of information.  See [template-pom](#template-pom) for more info.
3. I'm unsure how to sign - maybe I apply the configuration in `deps-deploy` to the `opts` provided to the `deploy` call?


## template-pom

1. Create a `template/pom.xml` 
2. Reference in `build.clj` `ci` function eg `(assoc opts :src-pom "template/pom.xml")`.

Lots of caveats

- The template file _requires_ the schema info on the `project` tag, otherwise the generated POM is unusable.
- When using the template file, clojars _requires_ `modelVersion` to be in the template.  Otherwise `bb/jar` doesn't know which version to specify.
- `bb/jar` does not generate `description`, `url`, or `scm` ... all of which are necessary to flesh out the clojars webview.  They must be included in the template.
- However you structure the version string, be sure to check `<scm><tag>xxx</tag></scm>` in the generated POM file.  This is how you need to tag the release in github.  If you don't do this, cljdoc won't work.
