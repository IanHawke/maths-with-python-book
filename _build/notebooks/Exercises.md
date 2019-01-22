---
redirect_from:
  - "/notebooks/exercises"
interact_link: content/notebooks/Exercises.ipynb
title: 'Exercises'
prev_page:
  url: /notebooks/11-more-classes
  title: 'Classes and OOP'
next_page:
  url: 
  title: ''
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---

Suggestions for lab exercises.

# Variables and assignment

## Exercise 1

Remember that $n! = n \times (n - 1) \times \dots \times 2 \times 1$. Compute $15!$, assigning the result to a sensible variable name.

## Exercise 2

Using the `math` module, check your result for $15$ factorial. You should explore the help for the `math` library and its functions, using eg tab-completion, the spyder inspector, or online sources.

## Exercise 3

[Stirling's approximation](http://mathworld.wolfram.com/StirlingsApproximation.html) gives that, for large enough $n$, 

\begin{equation}
  n! \simeq \sqrt{2 \pi} n^{n + 1/2} e^{-n}.
\end{equation}

Using functions and constants from the `math` library, compare the results of $n!$ and Stirling's approximation for $n = 5, 10, 15, 20$. In what sense does the approximation improve?

# Basic functions

## Exercise 1

Write a function to calculate the volume of a cuboid with edge lengths $a, b, c$. Test your code on sample values such as

1. $a=1, b=1, c=1$ (result should be $1$);
2. $a=1, b=2, c=3.5$ (result should be $7.0$);
3. $a=0, b=1, c=1$ (result should be $0$);
4. $a=2, b=-1, c=1$ (what do you think the result should be?).

## Exercise 2

Write a function to compute the time (in seconds) taken for an object to fall from a height $H$ (in metres) to the ground, using the formula
\begin{equation}
  h(t) = \frac{1}{2} g t^2.
\end{equation}
Use the value of the acceleration due to gravity $g$ from `scipy.constants.g`. Test your code on sample values such as

1. $H = 1$m (result should be $\approx 0.452$s);
2. $H = 10$m (result should be $\approx 1.428$s);
3. $H = 0$m (result should be $0$s);
4. $H = -1$m (what do you think the result should be?).

## Exercise 3

Write a function that computes the area of a triangle with edge lengths $a, b, c$. You may use the formula
\begin{equation}
  A = \sqrt{s (s - a) (s - b) (s - c)}, \qquad s = \frac{a + b + c}{2}.
\end{equation}

Construct your own test cases to cover a range of possibilities.

# Floating point numbers

## Exercise 1

Computers cannot, in principle, represent real numbers perfectly. This can lead to problems of accuracy. For example, if
\begin{equation}
  x = 1, \qquad y = 1 + 10^{-14} \sqrt{3}
\end{equation}
then it *should* be true that
\begin{equation}
  10^{14} (y - x) = \sqrt{3}.
\end{equation}
Check how accurately this equation holds in Python and see what this implies about the accuracy of subtracting two numbers that are close together.

## Exercise 2

The standard quadratic formula gives the solutions to

\begin{equation}
  a x^2 + b x + c = 0
\end{equation}

as

\begin{equation}
  x = \frac{-b \pm \sqrt{b^2 - 4 a c}}{2 a}.
\end{equation}

Show that, if $a = 10^{-n} = c$ and $b = 10^n$ then

\begin{equation}
  x = \frac{10^{2 n}}{2} \left( -1 \pm \sqrt{1 - 10^{-4n}} \right).
\end{equation}

Using the expansion (from Taylor's theorem)

\begin{equation}
  \sqrt{1 - 10^{-4 n}} \simeq 1 - \frac{10^{-4 n}}{2} + \dots, \qquad n \gg 1,
\end{equation}

show that

\begin{equation}
  x \simeq -10^{2 n} + \frac{10^{-2 n}}{4} \quad \text{and} \quad -\frac{10^{-2n}}{4}, \qquad n \gg 1.
\end{equation}

## Exercise 3

By multiplying and dividing by $-b \mp \sqrt{b^2 - 4 a c}$, check that we can also write the solutions to the quadratic equation as

\begin{equation}
  x = \frac{2 c}{-b \mp \sqrt{b^2 - 4 a c}}.
\end{equation}

## Exercise 4

Using Python, calculate both solutions to the quadratic equation

\begin{equation}
  10^{-n} x^2 + 10^n x + 10^{-n} = 0
\end{equation}

for $n = 3$ and $n = 4$ using both formulas. What do you see? How has floating point accuracy caused problems here?

## Exercise 5

The standard definition of the derivative of a function is

\begin{equation}
  \left. \frac{\text{d} f}{\text{d} x} \right|_{x=X} = \lim_{\delta \to 0} \frac{f(X + \delta) - f(X)}{\delta}.
\end{equation}

We can *approximate* this by computing the result for a *finite* value of $\delta$:

\begin{equation}
  g(x, \delta) = \frac{f(x + \delta) - f(x)}{\delta}.
\end{equation}

Write a function that takes as inputs a function of one variable, $f(x)$, a location $X$, and a step length $\delta$, and returns the approximation to the derivative given by $g$.

## Exercise 6

The function $f_1(x) = e^x$ has derivative with the exact value $1$ at $x=0$. Compute the approximate derivative using your function above, for $\delta = 10^{-2 n}$ with $n = 1, \dots, 7$. You should see the results initially improve, then get worse. Why is this?

# Prime numbers

## Exercise 1

Write a function that tests if a number is prime. Test it by writing out all prime numbers less than 50.

## Exercise 2

500 years ago some believed that the number $2^n - 1$ was prime for *all* primes $n$. Use your function to find the first prime $n$ for which this is not true.

## Exercise 3

The *Mersenne* primes are those that have the form $2^n-1$, where $n$ is prime. Use your previous solutions to generate all the $n < 40$ that give Mersenne primes.

## Exercise 4

Write a function to compute all prime factors of an integer $n$, including their multiplicities. Test it by printing the prime factors (without multiplicities) of $n = 17, \dots, 20$ and the multiplicities (without factors) of $n = 48$.

##### Note

One effective solution is to return a *dictionary*, where the keys are the factors and the values are the multiplicities.

## Exercise 5

Write a function to generate all the integer divisors, including 1, but not including $n$ itself, of an integer $n$. Test it on $n = 16, \dots, 20$.

##### Note

You could use the prime factorization from the previous exercise, or you could do it directly.

## Exercise 6

A *perfect* number $n$ is one where the divisors sum to $n$. For example, 6 has divisors 1, 2, and 3, which sum to 6. Use your previous solution to find all perfect numbers $n < 10,000$ (there are only four!).

## Exercise 7

Using your previous functions, check that all perfect numbers $n < 10,000$ can be written as $2^{k-1} \times (2^k - 1)$, where $2^k-1$ is a Mersenne prime.

## Exercise 8 (bonus)

Investigate the `timeit` function in python or IPython. Use this to measure how long your function takes to check that, if $k$ on the Mersenne list then $n = 2^{k-1} \times (2^k - 1)$ is a perfect number, using your functions. Stop increasing $k$ when the time takes too long!

##### Note

You could waste considerable time on this, and on optimizing the functions above to work efficiently. It is *not* worth it, other than to show how rapidly the computation time can grow!

# Logistic map

Partly taken from Newman's book, p 120.

The logistic map builds a sequence of numbers $\{ x_n \}$ using the relation

\begin{equation}
  x_{n+1} = r x_n \left( 1 - x_n \right),
\end{equation}

where $0 \le x_0 \le 1$.

## Exercise 1

Write a program that calculates the first $N$ members of the sequence, given as input $x_0$ and $r$ (and, of course, $N$).

## Exercise 2

Fix $x_0=0.5$. Calculate the first 2,000 members of the sequence for $r=1.5$ and $r=3.5$ Plot the last 100 members of the sequence in both cases.

What does this suggest about the long-term behaviour of the sequence?

## Exercise 3

Fix $x_0 = 0.5$. For each value of $r$ between $1$ and $4$, in steps of $0.01$, calculate the first 2,000 members of the sequence. Plot the last 1,000 members of the sequence on a plot where the $x$-axis is the value of $r$ and the $y$-axis is the values in the sequence. Do not plot lines - just plot markers (e.g., use the `'k.'` plotting style).

## Exercise 4

For iterative maps such as the logistic map, one of three things can occur:

1. The sequence settles down to a *fixed point*.
2. The sequence rotates through a finite number of values. This is called a *limit cycle*.
3. The sequence generates an infinite number of values. This is called *deterministic chaos*.

Using just your plot, or new plots from this data, work out approximate values of $r$ for which there is a transition from fixed points to limit cycles, from limit cycles of a given number of values to more values, and the transition to chaos.

# Mandelbrot

The Mandelbrot set is also generated from a sequence, $\{ z_n \}$, using the relation

\begin{equation}
  z_{n+1} = z_n^2 + c, \qquad z_0 = 0.
\end{equation}

The members of the sequence, and the constant $c$, are all complex. The point in the complex plane at $c$ is in the Mandelbrot set only if the $\|z_n\| < 2$ for all members of the sequence. In reality, checking the first 100 iterations is sufficient.

Note: the python notation for a complex number $x + \text{i} y$ is `x + yj`: that is, `j` is used to indicate $\sqrt{-1}$. If you know the values of `x` and `y` then `x + yj` constructs a complex number; if they are stored in variables you can use `complex(x, y)`.

## Exercise 1

Write a function that checks if the point $c$ is in the Mandelbrot set.

## Exercise 2

Check the points $c=0$ and $c=\pm 2 \pm 2 \text{i}$ and ensure they do what you expect. (What *should* you expect?)

## Exercise 3

Write a function that, given $N$

1. generates an $N \times N$ grid spanning $c = x + \text{i} y$, for $-2 \le x \le 2$ and $-2 \le y \le 2$;
2. returns an $N\times N$ array containing one if the associated grid point is in the Mandelbrot set, and zero otherwise.

## Exercise 4

Using the function `imshow` from `matplotlib`, plot the resulting array for a $100 \times 100$ array to make sure you see the expected shape.

## Exercise 5

Modify your functions so that, instead of returning whether a point is inside the set or not, it returns the logarithm of the number of iterations it takes. Plot the result using `imshow` again.

## Exercise 6

Try some higher resolution plots, and try plotting only a section to see the structure. **Note** this is not a good way to get high accuracy close up images!

# Equivalence classes

An *equivalence class* is a relation that groups objects in a set into related subsets. For example, if we think of the integers modulo $7$, then $1$ is in the same equivalence class as $8$ (and $15$, and $22$, and so on), and $3$ is in the same equivalence class as $10$. We use the tilde $3 \sim 10$ to denote two objects within the same equivalence class.

Here, we are going to define the positive integers programmatically from equivalent sequences.

## Exercise 1

Define a python class `Eqint`. This should be

1. Initialized by a sequence;
2. Store the sequence;
3. Define its representation (via the `__repr__` function) to be the integer length of the sequence;
4. Redefine equality (via the `__eq__` function) so that two `eqint`s are equal if their sequences have same length.

## Exercise 2

Define a `zero` object from the empty list, and three `one` objects, from a single object list, tuple, and string. For example

```python
one_list = Eqint([1])
one_tuple = Eqint((1,))
one_string = Eqint('1')
```

Check that none of the `one` objects equal the zero object, but all equal the other `one` objects. Print each object to check that the representation gives the integer length.

## Exercise 3

Redefine the class by including an `__add__` method that combines the two sequences. That is, if `a` and `b` are `Eqint`s then `a+b` should return an `Eqint` defined from combining `a` and `b`s sequences.

##### Note

Adding two different *types* of sequences (eg, a list to a tuple) does not work, so it is better to either iterate over the sequences, or to convert to a uniform type before adding.

## Exercise 4

Check your addition function by adding together all your previous `Eqint` objects (which will need re-defining, as the class has been redefined). Print the resulting object to check you get `3`, and also print its internal sequence.

## Exercise 5

We will sketch a construction of the positive integers from *nothing*.

1. Define an empty list `positive_integers`.
2. Define an `Eqint` called `zero` from the empty list. Append it to `positive_integers`.
3. Define an `Eqint` called `next_integer` from the `Eqint` defined by *a copy of* `positive_integers` (ie, use `Eqint(list(positive_integers))`. Append it to `positive_integers`.
4. Repeat step 3 as often as needed.

Use this procedure to define the `Eqint` equivalent to $10$. Print it, and its internal sequence, to check.

# Rational numbers

Instead of working with floating point numbers, which are not "exact", we could work with the rational numbers $\mathbb{Q}$. A rational number $q \in \mathbb{Q}$ is defined by the *numerator* $n$ and *denominator* $d$ as $q = \frac{n}{d}$, where $n$ and $d$ are *coprime* (ie, have no common divisor other than $1$).

## Exercise 1

Find a python function that finds the greatest common divisor (`gcd`) of two numbers. Use this to write a function `normal_form` that takes a numerator and divisor and returns the coprime $n$ and $d$. Test this function on $q = \frac{3}{2}$, $q = \frac{15}{3}$, and $q = \frac{20}{42}$.

## Exercise 2

Define a class `Rational` that uses the `normal_form` function to store the rational number in the appropriate form. Define a `__repr__` function that prints a string that *looks like* $\frac{n}{d}$ (**hint**: use `len(str(number))` to find the number of digits of an integer). Test it on the cases above.

## Exercise 3

Overload the `__add__` function so that you can add two rational numbers. Test it on $\frac{1}{2} + \frac{1}{3} + \frac{1}{6} = 1$.

## Exercise 4

Overload the `__mul__` function so that you can multiply two rational numbers. Test it on $\frac{1}{3} \times \frac{15}{2} \times \frac{2}{5} = 1$.

## Exercise 5

Overload the [`__rmul__`](https://docs.python.org/2/reference/datamodel.html?highlight=rmul#object.__rmul__) function so that you can multiply a rational by an *integer*. Check that $\frac{1}{2} \times 2 = 1$ and $\frac{1}{2} + (-1) \times \frac{1}{2} = 0$. Also overload the `__sub__` function (using previous functions!) so that you can subtract rational numbers and check that $\frac{1}{2} - \frac{1}{2} = 0$.

## Exercise 6

Overload the `__float__` function so that `float(q)` returns the floating point approximation to the rational number `q`. Test this on $\frac{1}{2}, \frac{1}{3}$, and $\frac{1}{11}$.

## Exercise 7

Overload the `__lt__` function to compare two rational numbers. Create a list of rational numbers where the denominator is $n = 2, \dots, 11$ and the numerator is the floored integer $n/2$, ie `n//2`. Use the `sorted` function on that list (which relies on the `__lt__` function).

## Exercise 8

The [Wallis formula for $\pi$](http://mathworld.wolfram.com/WallisFormula.html) is

\begin{equation}
  \pi = 2 \prod_{n=1}^{\infty} \frac{ (2 n)^2 }{(2 n - 1) (2 n + 1)}.
\end{equation}

We can define a partial product $\pi_N$ as

\begin{equation}
  \pi_N = 2 \prod_{n=1}^{N} \frac{ (2 n)^2 }{(2 n - 1) (2 n + 1)},
\end{equation}

each of which are rational numbers.

Construct a list of the first 20 rational number approximations to $\pi$ and print them out. Print the sorted list to show that the approximations are always increasing. Then convert them to floating point numbers, construct a `numpy` array, and subtract this array from $\pi$ to see how accurate they are.

# The shortest published Mathematical paper

A [candidate for the shortest mathematical paper ever](http://www.ams.org/journals/bull/1966-72-06/S0002-9904-1966-11654-3/S0002-9904-1966-11654-3.pdf) shows the following result:

\begin{equation}
  27^5 + 84^5 + 110^5 + 133^5 = 144^5.
\end{equation}

This is interesting as

> This is a counterexample to a conjecture by Euler ... that at least $n$ $n$th powers are required to sum to an $n$th power, $n > 2$.

## Exercise 1

Using python, check the equation above is true.

## Exercise 2

The more interesting statement in the paper is that

\begin{equation}
  27^5 + 84^5 + 110^5 + 133^5 = 144^5.
\end{equation}

> [is] the smallest instance in which four fifth powers sum to a fifth power.

Interpreting "the smallest instance" to mean the solution where the right hand side term (the largest integer) is the smallest, we want to use python to check this statement.

You may find the `combinations` function from the `itertools` package useful.



{:.input_area}
```python
import numpy
import itertools
```


The `combinations` function returns all the combinations (ignoring order) of `r` elements from a given list. For example, take a list of length 6, `[1, 2, 3, 4, 5, 6]` and compute all the combinations of length 4:



{:.input_area}
```python
input_list = numpy.arange(1, 7)
combinations = list(itertools.combinations(input_list, 4))
print(combinations)
```


{:.output .output_stream}
```
[(1, 2, 3, 4), (1, 2, 3, 5), (1, 2, 3, 6), (1, 2, 4, 5), (1, 2, 4, 6), (1, 2, 5, 6), (1, 3, 4, 5), (1, 3, 4, 6), (1, 3, 5, 6), (1, 4, 5, 6), (2, 3, 4, 5), (2, 3, 4, 6), (2, 3, 5, 6), (2, 4, 5, 6), (3, 4, 5, 6)]

```

We can already see that the number of terms to consider is large.

Note that we have used the `list` function to explicitly get a list of the combinations. The `combinations` function returns a *generator*, which can be used in a loop as if it were a list, without storing all elements of the list.

How fast does the number of combinations grow? The standard formula says that for a list of length $n$ there are

\begin{equation}
  \begin{pmatrix} n \\ k \end{pmatrix} = \frac{n!}{k! (n-k)!}
\end{equation}

combinations of length $k$. For $k=4$ as needed here we will have $n (n-1) (n-2) (n-3) / 24$ combinations. For $n=144$ we therefore have



{:.input_area}
```python
n_combinations = 144*143*142*141/24
print("Number of combinations of 4 objects from 144 is {}".format(n_combinations))
```


{:.output .output_stream}
```
Number of combinations of 4 objects from 144 is 17178876

```

### Exercise 2a

Show, by getting python to compute the number of combinations $N = \begin{pmatrix} n \\ 4 \end{pmatrix}$ that $N$ grows roughly as $n^4$. To do this, plot the number of combinations and $n^4$ on a log-log scale. Restrict to $n \le 50$.

With 17 million combinations to work with, we'll need to be a little careful how we compute.

One thing we could try is to loop through each possible "smallest instance" (the term on the right hand side) in increasing order. We then check all possible combinations of left hand sides.

This is computationally *very expensive* as we repeat a lot of calculations. We repeatedly recalculate combinations (a bad idea). We repeatedly recalculate the powers of the same number.

Instead, let us try creating the list of all combinations of powers once.

### Exercise 2b

1. Construct a `numpy` array containing all integers in $1, \dots, 144$ to the fifth power. 
2. Construct a list of all combinations of four elements from this array.
3. Construct a list of sums of all these combinations.
4. Loop over one list and check if the entry appears in the other list (ie, use the `in` keyword).

# Lorenz attractor

The Lorenz system is a set of ordinary differential equations which can be written

\begin{equation}
  \frac{\text{d} \vec{v}}{\text{d} \vec{t}} = \vec{f}(\vec{v})
\end{equation}

where the variables in the state vector $\vec{v}$ are

\begin{equation}
  \vec{v} = \begin{pmatrix} x(t) \\ y(t) \\ z(t) \end{pmatrix}
\end{equation}

and the function defining the ODE is

\begin{equation}
  \vec{f} = \begin{pmatrix} \sigma \left( y(t) - x(t) \right) \\ x(t) \left( \rho - z(t) \right) - y(t) \\ x(t) y(t) - \beta z(t) \end{pmatrix}.
\end{equation}

The parameters $\sigma, \rho, \beta$ are all real numbers.

## Exercise 1

Write a function `dvdt(v, t, params)` that returns $\vec{f}$ given $\vec{v}, t$ and the parameters $\sigma, \rho, \beta$.

## Exercise 2

Fix $\sigma=10, \beta=8/3$. Set initial data to be $\vec{v}(0) = \vec{1}$. Using `scipy`, specifically the `odeint` function of `scipy.integrate`, solve the Lorenz system up to $t=100$ for $\rho=13, 14, 15$ and $28$.

Plot your results in 3d, plotting $x, y, z$.

## Exercise 3

Fix $\rho = 28$. Solve the Lorenz system twice, up to $t=40$, using the two different initial conditions $\vec{v}(0) = \vec{1}$ and $\vec{v}(0) = \vec{1} + \vec{10^{-5}}$.

Show four plots. Each plot should show the two solutions on the same axes, plotting $x, y$ and $z$. Each plot should show $10$ units of time, ie the first shows $t \in [0, 10]$, the second shows $t \in [10, 20]$, and so on.

This shows the *sensitive dependence on initial conditions* that is characteristic of chaotic behaviour.
