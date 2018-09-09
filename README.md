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

  
