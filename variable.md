
Variables
---

You can try the code below in Lumo.

To define a variable:

```clojure
(def a 1)
; #'cljs.user/a
```

Or to create a local binding:

```clojure
(let [x 1
      y 2]
  (+ x y))
; 3
```

Normally, you don't modify the value of a variable. To define a variable to a changing state, use the type `Atom`:

```clojure
(def b (atom 1))
; #'cljs.user/b
```

A reference to the Atom is returned. To read the value of the reference, use `@b`, which means `(deref b)`.
We prefer to name the variable as `*b` to indicates it's changing state. And to change the value:

```clojure
(def *b (atom 1))
; #'cljs.user/b
(reset! *b 2)
; 2
```

There's another use case in building apps. To cooperate with hot code swapping, we use `defonce` to persist the state during code swapping:

```clojure
(defonce *c (atom 1))
; #'cljs.user/*c
```
