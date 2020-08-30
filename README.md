# Clojourney

Repo where I'll document and share my advancements in learning
- [Clojourney](#clojourney)
  - [Language spec/themes](#language-specthemes)
  - [Exercism exercises](#exercism-exercises)
    - [Two-fer](#two-fer)
      - [Iteration #0](#iteration-0)
      - [Iteration #1](#iteration-1)
    - [Reverse-string](#reverse-string)
      - [Iteration #0](#iteration-0-1)
      - [Iteration #1](#iteration-1-1)
      - [Iteration #2](#iteration-2)
      - [Iteration #3](#iteration-3)
      - [Iteration #4](#iteration-4)
      - [Iteration #5](#iteration-5)
      - [Iteration #6](#iteration-6)
      - [Todo:](#todo)
    - [Accumulate](#accumulate)
      - [Iteration #0](#iteration-0-2)
    - [Beer-song](#beer-song)
      - [Iteration #0](#iteration-0-3)
## Language spec/themes

TBD.

## Exercism exercises

Resource where I'll post the iterations of [exercism](https://exercism.io/my/tracks/clojure) Clojure track exercises (mostly based on feedback by code mentors, to whom I'm grateful).

### Two-fer 

#### Iteration #0
```clojure
(ns two-fer)

(defn two-fer
  ([] "One for you, one for me.)
  ([name] (str "One for " name  ", one for me.")))
```

#### Iteration #1
```clojure
(ns two-fer)

(defn two-fer
  ([] (two-fer "you")) ; define diffferent arities to simulate "default arguments"
  ([name] (str "One for " name  ", one for me.")))
```

### Reverse-string


#### Iteration #0
```clojure
(ns reverse-string)

(defn reverse-string [s]
  (reduce str
          (map (fn [idx] (str (get s (- (- (count s) 1) idx))))
               (range (count s)))))
```
#### Iteration #1
```clojure
(ns reverse-string)

(defn reverse-string [s]
  (reduce str
          (map (fn [idx] (str (get s idx)))
               (range (count s) -1 -1)))) ; use begin, end and step params
```
#### Iteration #2
```clojure
(ns reverse-string)

(defn reverse-string [s]
  (reduce str
          (map (fn [idx] (str (nth s idx))) ; change `get` for `nth`
               (range (- (count s) 1) -1 -1))))
```
#### Iteration #3
```clojure
(ns reverse-string)

(defn reverse-string [s]
  (reduce str
          (map (fn [idx] (str (nth s idx)))
               (range (dec (count s)) -1 -1)))); change (- x 1) for (dec x) 
```
#### Iteration #4
```clojure
(ns reverse-string)

(defn reverse-string [s]
  (reduce str
          (map #(str (nth s %)) ; change anonymous function for reader syntax
               (range (dec (count s)) -1 -1))))
```
#### Iteration #5
```clojure
(ns reverse-string)

(defn reverse-string [s]
  (reduce str
          (map #(nth s %) ; remove call to `str` from mapping fn
               (range (dec (count s)) -1 -1))))
```
#### Iteration #6
```clojure
(ns reverse-string)

(defn reverse-string [s]
  (apply str ; no need to reduce, can apply str to compact list of chars
         (map #(nth s %)
              (range (dec (count s)) -1 -1))))
```

#### Todo:
* solve without depending on strings' support for random access;

### Accumulate

#### Iteration #0

```clojure
(ns accumulate)

(defn accumulate [fn_ list_]
  (map fn_ list_)
  )
```

### Beer-song

#### Iteration #0

```clojure
(ns beer-song)

(defn bottles-in-wall [expression]
  (str expression " of beer on the wall"))

(defn base-verse [args]
  (str (bottles-in-wall (nth args 0)) ", " (nth args 1) " of beer.\n"
       "Take " (nth args 2) " down and pass it around, " (bottles-in-wall (nth args 3)) ".\n"))

(defn singular
  "Return the singular verse of the song"
  ([] ["1 bottle" "1 bottle" "it" "no more bottles"]))

(defn is-one? [num_] (= num_ 1))

(defn bottle-expression [num_]
  (if (is-one? num_)
    (str num_ " bottle")
    (str num_ " bottles")))

(defn plural
  "Return a plural verse of the song"
  ([num_]  [(bottle-expression num_) (bottle-expression num_) "one" (bottle-expression (dec num_))]))

(defn in-stock [num_]
  (if (is-one? num_)
    (base-verse (singular))
    (base-verse (plural num_))))

(defn out-of-stock
  ([] (str "No more bottles of beer on the wall, no more bottles of beer.\n"
           "Go to the store and buy some more, 99 bottles of beer on the wall.\n")))

(defn is-zero? [num_] (= num_ 0))

(defn verse
  ([num_]
   (if (is-zero? num_)
     (out-of-stock)
     (in-stock num_))))

(defn sing
  ([start] (sing start 0))
  ([start end] (apply str (drop-last (apply str  (map #(str % "\n") (map verse (range start (dec end) -1)))))))) ; drop last \n due to test case
```