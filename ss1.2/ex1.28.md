
### Miller-Rabin test
- premise
  - `n`
    - a prime number
  - `a`
    - any positive integer
    - a < n
- `a ^ n-1 ≡ 1 (modulo n)` filled for any a
  - sample: when n = 7
    ```
    2 ^ 6 : 64 % 7 = 1
    3 ^ 6 : 729 % 7 = 1
    4 ^ 6 : 4096 % 7 = 1
    5 ^ 6 : 15625 % 7 = 1
    6 ^ 6 : 46656 % 7 = 1
    ```
  - sample: when n = 6
    ```
    1 ^ 5 :  1 % 6 = 1
    2 ^ 5 :  32 % 6 = 2
    3 ^ 5 :  243 % 6 = 3
    4 ^ 5 :  1024 % 6 = 4
    5 ^ 5 :  3125 % 6 = 5
    ```

### expmod definiton
```s
(define (expmod base exp m)
    (display base) (display " ") (display exp) (display " ") (display m)
    (newline)
    (cond ((= exp 0) 1)
          ((even? exp)
            (remainder
              (square (expmod base (/ exp 2) m))
              m))
          (else
            (remainder
              (* base (expmod base (- exp 1) m))
              m))))
```

if n has x like this, n is **not prime**
  - x != 1 or n-1
    - if x = 1 or n - 1, x is **trivial** square root of 1
  - x ^ 2 mod n = 1

```s
(define (nontrivial-sqrt-of-1? n x)
  (and
      (or
        (not (= x 1))
        (not (= x (- n 1))))
      (= (modulo (square x) n) 1)))
```

if I check expmod result,
```s
(define (check n)
  (define (iter n a)
    (= (expmod a n (- n 1) 1)))
```

```s
(define (check-and-expmod base exp m)
  (cond ((= exp 0) 1)
        ((even? exp)
          (square-check
            (expmod base (/ exp 2) m)
            m))
        (else
          (remainder
            (* base (expmod base (- exp 1) m))
            m))))
(define (square-check x m))
```
