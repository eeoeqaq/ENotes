deplicate them before evaluate them
```scheme
(define (_a1 expr)
    (+ expr 1))

(define-macro (_a2 expr)
    `(+ ,expr 1))
  

(define-macro (ture1? expr)
    (list 'if expr
            ''passed
            (list 'quote ( list 'failed: expr))))

(define (ture2? expr)
    (list 'if expr
            ''passed
            (list 'quote(list 'failed: expr))))

(define (ture3? expr)
    (if expr
        'passed
        'failed:expr))

;;omitted the quotation and eval.
(true1? (> 1 0))
(eval(true2? '(> 1 0)))
  
  
(define (map x fn)
    (if (null? x)
        nil
        (cons (fn (car x))
            (map (cdr x) fn))))

;;what do we want a macro expand to???
;;(for x '(1 2 3 4) (* x x))  
;;(map '(1 2 3 4) (lambda (x) (* x x)))
(define-macro (for sym vals expr)
    (list 'map vals (list 'lambda (list sym) expr)))
  
  
(define (fact x)
    (if (= x 0)
        1
        (* x (fact (- x 1)))))

(define-macro (trace expr) ;;(trace (fact 5))
     (define operator (car expr))
    `(begin
        (define original ,operator)
        (define ,operator
            (lambda (n) (print (list (quote ,operator) n)) (original n)))
        (define result ,expr)
        (define ,operator original)
        result))
```
`

