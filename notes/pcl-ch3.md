# Practical Common Lisp: Chapter 3
## Practical: A Simple Database

&nbsp;

## Keyword Parameters
Keyword parameters (`&key`) allow you to write functions that can be called with a varying number of arguments.

- the value of the variables (`a`, `b`, and `c` in [Examples](#keyword_examples))  are bound to the values that follow the corresponding keyword

- if a particular keyword is not present in the call, the corresponding var is set to `NIL`
	
- in order to determine if  `NIL` was explicitly passed or just assigned if no value was present for the corresponding keyword, you can use a _supplied-p_ parameter.

<a name=keyword_examples></a>
#### Example

- `(defun foo (&key a b c) (list a b c))`

- `(defun foo (&key a (b 20) (c 30 c-p)) (list a b c c-p))` 
(with defaults and _supplied-p_ params)

~~~lisp
(foo :a 1 :b 2 :c 3)  ==> (1 2 3 T)
(foo :c 3 :b 2 :a 1)  ==> (1 2 3 T)
(foo :a 1 :c 3)       ==> (1 20 3 T)
(foo)                 ==> (NIL 20 30 NIL)
~~~

### &rest

Like `&key`, `&rest` modifies the way arguments are parsed. With a `&rest` in its parameter list, a function or macro can take an arbitrary number of arguments, which are collected into a single list that becomes the value of the variable whose name follows the `&rest`.

#### Example
~~~lisp
TODO
~~~

&nbsp;

## Macros
Lisp macros are like “code generators” that run automatically by the compiler. 

When a Lisp expression contains a call to a macro, instead of evaluating the arguments and passing them to the function, the Lisp compiler passes the arguments, unevaluated, to the macro code, which returns a new Lisp expression that is then evaluated in place of the original macro call.

A macro is just another mechanism for creating abstractions – specifically, at the syntactic level.

#### Example

`(defmacro backwards (expr) (reverse expr))`

~~~lisp
(backwards ("hello, world" t format))
> hello, world
> NIL
~~~

The call to `backwards` essentially converts into:

~~~lisp
(format t "hello, world”)
~~~

&nbsp;

## Notes
- `mapcar` is the typical `map` function

- `remove-if-not`  & `remove-if` are typical `filter` functions

- when using `MACROEXPAND-1`, followed by a macro, it'll call the macro code with appropriate arguments and return the expansion

- single quotes (`’`) stop Lisp from evaluating a form (a keyword, e.g. `’equal`)

- a back quote (``` ` ```) before an expression stops evaluation just like a forward quote, **but any subexpression that’s preceded by a comma**
(`,`) **is evaluated**

	#### Example

	~~~lisp
	`(1 2 (+ 1 2))        ==> (1 2 (+ 1 2))
	`(1 2 ,(+ 1 2))       ==> (1 2 3)
	~~~
	
<br>

- `,@` “splices” the value of the following expression (which must evaluate to a list) into the an enclosing list; it "breaks" off the elements of the list and returns them to the current list

	#### Example
	
	~~~lisp
	`(and ,(list 1 2 3))   ==> (AND (1 2 3))
	`(and ,@(list 1 2 3))  ==> (AND 1 2 3)
	`(and ,@(list 1 2 3) 4) ==> (AND 1 2 3 4)
	~~~