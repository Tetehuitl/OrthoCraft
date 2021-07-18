---
date updated: '2021-07-16T00:59:27-04:00'

---

 # Y and Z combinators in Javascript — Lambda Calculus with real code
- <https://medium.com/swlh/y-and-z-combinators-in-javascript-lambda-calculus-with-real-code-31f25be934ec>
- ![1*e6FuOl6VvFZYphZ7LW16Fw.png](Y%20and%20Z%20combinators%20in%20Javascript%20Lambda%20Calculus%20/1e6FuOl6VvFZYphZ7LW16Fw.png)
- Can you do recursion using only Javascript anonymous functions?
- Certainly. Here the Factorial of a number in one line
```
const fact = x => (x === 0 ? 1 : x * fact(x - 1));
```

- No, no. This is not anonymous. You name the function **fact** via a Javascript `const` and reference it within itself. I mean really anonymous, something like

```
(...params) => { // do stuff }
```

- with no variables at all, no self references, no state, just pure functions. Can you do this?
- Well, according to Lambda Calculus you can, using what are called _Fixed-Point Combinators_.
- Let’s see them in action using real Javascript code.
- In a very simple way, we can say that a Lambda Calculus is based on the use of unary functions, which mean functions with one parameter. Lambda functions are expressed in the form of `λx.y`, where `x` is the variable of the function and `y` is its body. Things like `λx.y` are called _Lambda abstractions_ in Lambda calculus theory.
- Therefore the natural translation of Lambda abstractions to Javascript are anonymous functions. Some examples

```
x => x          // λx.x        aka identity function
x => y => y(x)  // λx.λy.y(x)  y applied to x, where y is a function
x => x(x)       // λx.xx       apply a function x to itself
```
- For the purpose of this blog this is all we need to know about the theory. Let’s get to the code.
- This is the Y combinator expressed as Lambda abstraction
```
Y = λg. (λx. g (x x)) (λx. g (x x))
```

- And this is its equivalent in Javascript

```
const Y = g => (x => g(x(x)))(x => g(x(x)))
```

- Note: even if we use the variable `Y`, we are not using a named function, since `Y` is never referenced anywhere. We do define `Y` just for convenience and reduce verbosity.
- If we pass a function `f` as argument to `Y`, simply evaluating the Javascript code we obtain the following
- The fact that **`Y(f) = f(Y(f))`** makes **`Y`** a _fixed-point combinator_. We do not enter the theory of what _fixed-point combinators_ are. We just say that they are crucial for the implementation of recursion in Lambda calculus, and we see now why with an example.
- Do you remember the initial named function to compute the factorial?

```
const fact = x => (x === 0 ? 1 : x * fact(x - 1));
```
- we can abstract **`fact`** into a variable and create a new function **`F`** like this

```
F = f => x => (x === 0 ? 1 : x * f(x - 1))
```
- If we pass **`F`** to `Y` we obtain a new function **`fact'`**

```
fact' = Y(F)
```
- `Y` is a _fixed-point combinator_. Y has the property that **`Y(f) = f(Y(f))`**. So also the following holds

```
fact' = Y(F) = F(Y(F)) = F(fact')
```
- So, based on the fact that **`fact’** = F(**fact’)**`, we calculate **`fact’(2)`**, just for fun

```
fact’(2) = (F(fact'))(2)
 |
 = (f => x => (x === 0 ? 1 : x * f(x - 1))(fact'))(2)
 |
 = (x => (x === 0 ? 1 : x * fact'(x - 1)))(2)
 |
 = 2 === 0 ? 1 : 2 * fact'(2 - 1)
 |
 = 2 * fact'(1)
```
- See the magic? Just for the fact that `Y` is a _fixed-point combinator_ it implements recursion, as long as we pass to it a function in the format of `F`.
- Now we are all setup to code our Factorial recursion and check the result.
- What? Why `try catch`?
- Well, the whole thing does not work. It blows with `Maximum call stack size exceeded` error.
- But why? The reason is that Javascript adopts a _strict/eager evaluation strategy_ while the Y combinator expects a _lazy strategy_.
- But, apart from these definitions, it is interesting to look at what happens in the code. To make things simpler to reason about, let’s look at `Y` expressed in terms of a regular Javascript function.
- When `Y` is invoked with `F` as the argument, following happens (see the below diagram for reference).
- 1. Two unary functions, `innerYfunction1` and `innerYfunction2`, are declared within the scope of `Y` — such functions reference the F function passed in as parameter but, as we will see, this is not relevant to determine what is going to happen
- 2. `innerYfunction1` is invoked with `innerYfunction2` as its parameter
- 3. `innerYfunction1` starts its execution evaluating **`x(x)`** where the value of `x` is the value of the parameter passed in, i.e. it is `innerYfunction2`
- 4. `innerYfunction2` starts its execution with itself as its parameter and the first thing it does is to evaluate **`x(x)`** where the value of `x` is `innerYfunction2` itself — but as we have just seen, this turns out to invoke the execution of `innerYfunction2` with itself as parameter, which is what generates the infinite loop leading to _Maximum call stack size exceeded_
- So, are we left hopeless if the Y combinator can not work in Javascript? No, there are other fixed-points combinators that can come to our rescue.
- This is the definition of the Z combinator expressed as Lambda abstraction

```
Z = λg.(λx.g(λv.xxv))(λx.g(λv.xxv))
```
- and this is its Javascript implementation

```
- const Z = g => (x => g(v => x(x)(v)))(x => g(v => x(x)(v)))
```
- If we evaluate `Z` passing it a function `f` we obtain the following
- So, for the `Z` combinator, the following holds true

```
Z(f) = f(v => Z(f)(v))
```
- We can use the same example we used with the Y combinator to prove that `Z` actually allows us to implement recursive logic using pure anonymous functions.
- Starting from the factorial logic, we create the **`fact’’`** function using the Z combinator rather then the Y combinator as in the previous example.

```
const fact = x => (x === 0 ? 1 : x * fact(x - 1));
F = f => x => (x === 0 ? 1 : x * f(x - 1));
fact'' = Z(F) = F(v => Z(F)(v)) = F(v => fact''(v))
```
- Now we calculate **`fact’’**(2)`

```
fact''(2) = F(v => fact''(v)) (2)
 |
 = (f => x => x === 0 ? 1 : x*f(x-1))(v => fact''(v)) (2)
 |
 = (x => x === 0 ? 1 : x*(v => fact''(v))(x-1)) (2)
 |
 = 2 === 0 ? 1 : 2 * (v => fact''(v))(2-1)
 |
 = 2 * (v => fact''(v))(1)
 |
 = 2 * fact''(1)
```
- See the magic again? So the Z combinator does the same as the Y combinator. The difference is that it introduces a function in its definition instead of a direct calculation of an expression.
- And this function is what makes it digestible for a ‘strict’ language as Javascript. Looking at the Z combinator defined using regular Javascript functions can help clarify this last point.
- Can you do recursion using only Javascript anonymous functions?
- Yes we can. And this is the code
- `F` and `Z` are not named functions, in the sense they are not self referenced. They are just placeholders to help clarify what we are doing.
- Replacing `F` and `Z` with their definition we obtain the equivalent version
- And if we execute this `fibonacci(n)` function with a natural number we get the right result

```
console.log(fibonacci(10))  // prints 89
```
- Is there any practical use of these Javascript combinators in Production code? Well…. probably not. Performance wise they can be much worse if compared to implementations which use self-referencing functions, and it is hard to say that the code is clearer to read and reason about.
- But they still are interesting things to analyse.
- If, for whatever reason, you want to enter the Lambda Calculus world, going through a real code implementation may help you grasp its mechanics in a concrete way.
- It is a good way to exercise you functional programming skills.
- And, more than everything else, there is a bit of magic going on behind the scenes. This magic has been discovered, not invented. This magic was there in the world of logic before Alonzo Church and Haskel Curry.
- Some more reasoning about Lambda Calculus implemented in Javascript can be [read here](https://hackernoon.com/lets-code-the-roots-of-functional-programming-lambda-calculus-implemented-in-typescript-36806ebc2857). The code shown and more Lambda Calculus examples are in [this repo](https://github.com/EnricoPicci/lambda-calculus-typescript).
