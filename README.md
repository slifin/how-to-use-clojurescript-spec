# How to use Clojurescript spec

Ensure you have lein installed:


```
apt install lein
brew install lein
choco install lein
```

Open your terminal and move to the directory above where you'd like your project to reside. 

Run ```lein new figwheel spec-test``` 

Open ```spec-test/project.cljs``` in a text editor

Navigate to https://github.com/clojure/spec.alpha 

Copy the "Leiningen dependency information:" section
and add the information to your dependencies list in project.cljs

Repeat the process with https://github.com/clojure/test.check

At the end of the process you should have something similar to this in your project.cljs

```
:dependencies [[org.clojure/clojure "1.9.0"]
               [org.clojure/clojurescript "1.10.238"]
               [org.clojure/core.async  "0.4.474"]
               [org.clojure/spec.alpha "0.2.176"]
               [org.clojure/test.check "0.10.0-alpha3"]]
```

Run ```lein fighwheel``` in the terminal to see the result of the work in realtime

Open ```spec-test/src/spec_test/core.cljs``` in a text editor

Add the spec library by changing the first declaration from

```
(ns spec-test.core
    (:require ))
```
to 
```
(ns spec-test.core
    (:require [clojure.spec.alpha :as spec]
    	[clojure.spec.test.alpha :as test]))
```

Delete everything else in the file

Create a new function 

```
(defn foo [x]
  (inc x))
```

Create a spec for the function 
```
(spec/fdef foo
  :args (spec/cat :x number?)
  :ret number?)
```

Tell Clojurescript to replace all function calls after this point with calls that 
check the inputs to the function first with specs.
```
(test/instrument)
```

Run the function call:
```
(foo "hey")
```

If everything has worked there will be an uncaught exception in the browser developer console

```
Call to #'spec-test.core/foo did not conform to spec:
In: [0] val: "hey" fails at: [:args :x] predicate: number?
```


## Notes

```(test/instrument)``` Is not magic, it will not check data that has been spec'd
unless it passes through a function that does have a spec, it is context sensitive
it will not be able to validate functions that have yet to be defined or do not yet
have specifications in the chronology of the program

Function calls need to happen after ```(test/instrument)``` to be checked
