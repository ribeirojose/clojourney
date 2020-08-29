# Clojourney

Repo where I'll document and share my advancements in learning clojure.
- [Clojourney](#clojourney)
  - [Language spec/themes](#language-specthemes)
  - [Exercism exercises](#exercism-exercises)
    - [Two-fer](#two-fer)
      - [Iteration #1](#iteration-1)
      - [Iteration #2](#iteration-2)
    - [Reverse-string](#reverse-string)
      - [Iteration #1](#iteration-1-1)
      - [Iteration #2](#iteration-2-1)
      - [Iteration #3](#iteration-3)
      - [Iteration #4](#iteration-4)
      - [Iteration #5](#iteration-5)
      - [Iteration #6](#iteration-6)
      - [Iteration #7](#iteration-7)
      - [Todo:](#todo)
## Language spec/themes

TBD.

## Exercism exercises

Resource where I'll post the iterations of [exercism](https://exercism.io/my/tracks/clojure) Clojure track exercises (mostly based on feedback by code mentors, to whom I'm grateful).

### Two-fer 

#### Iteration #1
```clojure
(ns two-fer)

(defn two-fer
  ([] "One for you, one for me.)
  ([name] (str "One for " name  ", one for me.")))
```

#### Iteration #2
```clojure
(ns two-fer)

(defn two-fer
  ([] (two-fer "you")) ; define diffferent arities to simulate "default arguments"
  ([name] (str "One for " name  ", one for me.")))
```

### Reverse-string


#### Iteration #1
```clojure
(ns reverse-string)

(defn reverse-string [s]
  (reduce str
          (map (fn [idx] (str (get s (- (- (count s) 1) idx))))
               (range (count s)))))
```
#### Iteration #2
```clojure
(ns reverse-string)

(defn reverse-string [s]
  (reduce str
          (map (fn [idx] (str (get s idx)))
               (range (count s) -1 -1)))) ; use begin, end and step params
```
#### Iteration #3
```clojure
(ns reverse-string)

(defn reverse-string [s]
  (reduce str
          (map (fn [idx] (str (nth s idx))) ; change `get` for `nth`
               (range (- (count s) 1) -1 -1))))
```
#### Iteration #4
```clojure
(ns reverse-string)

(defn reverse-string [s]
  (reduce str
          (map (fn [idx] (str (nth s idx)))
               (range (dec (count s)) -1 -1)))); change (- x 1) for (dec x) 
```
#### Iteration #5
```clojure
(ns reverse-string)

(defn reverse-string [s]
  (reduce str
          (map #(str (nth s %)) ; change anonymous function for reader syntax
               (range (dec (count s)) -1 -1))))
```
#### Iteration #6
```clojure
(ns reverse-string)

(defn reverse-string [s]
  (reduce str
          (map #(nth s %) ; remove call to `str` from mapping fn
               (range (dec (count s)) -1 -1))))
```
#### Iteration #7
```clojure
(ns reverse-string)

(defn reverse-string [s]
  (apply str ; no need to reduce, can apply str to compact list of chars
         (map #(nth s %)
              (range (dec (count s)) -1 -1))))
```

#### Todo:
* solve without depending on strings' support for random access;