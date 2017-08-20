
Installation
----

The compiler of ClojureScript is implemented in Java, in most cases you need to compile cljs with toolchains based on JVM. But now you can also compile it with Lumo or Planck, which are based on self-hosted ClojureScript.

In this guide, we suggest using Lumo as the REPL, and shadow-cljs as the compiler.

### Lumo

https://github.com/anmonteiro/lumo

> Lumo is a standalone ClojureScript environment that runs on Node.js and the V8 JavaScript engine.

Lumo is based on Node.js , so it's possible to use npm modules, to install Lumo:

```bash
brew install lumo
```

Just like `node`, you can start a REPL or evaluate a file with the command `lumo`:

```bash
$ lumo
Lumo 1.4.1
ClojureScript 1.9.521
Node.js v7.9.0
 Docs: (doc function-name-here)
 Exit: Control+D or :cljs/quit or exit

cljs.user=> (println "demo")
demo
nil
cljs.user=>
```

Let's say `demo.cljs` looks like:

```clojure
(println "this is a demo")
(println (+ 1 2))

(def a 1)
(println a)
```

Then we get:

```bash
=>> lumo demo.cljs
this is a demo
3
1
```

### shadow-cljs

https://github.com/thheller/shadow-cljs

> shadow-cljs provides everything you need to compile your ClojureScript code with a focus on simplicity and ease of use.

shadow-cljs is based on JVM but it takes care of JVM by itself, so it appears to be more friendly to non-JVM developers. shadow-cljs can be installed by simply run:

```bash
npm install -g shadow-cljs
```

shadow-cljs' configuration file is called `shadow-cljs.edn`, for example:

```edn
{:source-paths ["src"]
 :dependencies []
 :builds {:app {:output-dir "target/"
                :asset-path "."
                :target :browser
                :modules {:main {:entries [app.main]}}
                :devtools {:after-load app.main/reload!}}}}
```

Then, to watch/compile/reload cljs code in `src`, just run:

```bash
shadow-cljs watch app
```

To build the project for production, run:

```bash
shadow-cljs release app
```

This `app` in the command like corresponds to the `:build-id` called `:app`.

To be noticed, shadow-cljs do use JVM, so you may either have a Java environment installed, or shadow-cljs will install `node-jre` to provide JVM. To download Java, open http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html .

### Other tools

There are other tools to compile ClojureScript: Boot, Lein, Planck, or even call Java APIs directly. Try them if you are interested.
