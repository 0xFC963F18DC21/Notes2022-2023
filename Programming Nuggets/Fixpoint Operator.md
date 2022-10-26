The fixpoint operator, also known as the Y-combinator, is a useful construct that allows the use of recursion in languages where functions cannot directly reference themselves by name.

A typical deferred-recursion function would probably have a type similar to a continuation-passing function, but with the "recursive call" as the first argument. E.g. A recursive factorial implementation written in this way would look something like:

```
fact(rec: int -> int, n: int): int
  | n <= 1 => 1
  | else   => rec(n - 1)
```

It is not quite as useful in most programming languages, but they are still fun to try and implement, so here are a few of them!

**Haskell**:
```haskell
fix :: (a -> a) -> a
fix f = f (fix f)
```

**Racket**:
```scheme
(define ((fix f) . args)
  (apply f (fix f) args))
```

**Python**:
```python
def fix(f):
  def fixed(*args, **kwargs):
    return f(fix(f), *args, **kwargs)
  return fixed
```

**Clojure**:
```clojure
(defn fix [f]
  (fn [& args]
    (apply f (fix f) args)))
```
