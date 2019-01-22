---
interact_link: content/07-sympy.ipynb
title: 'Symbolic Python'
prev_page:
  url: /06-numpy-plotting
  title: 'Scientific Python'
next_page:
  url: /08-statistics
  title: 'Statistics'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---

# Symbolic Python

In standard mathematics we routinely write down abstract variables or concepts and manipulate them without ever assigning specific values to them. An example would be the quadratic equation

$$  a x^2 + b x + c = 0 $$

and its roots $x_{\pm}$: we can write down the solutions of the equation and discuss the existence, within the real numbers, of the roots, without specifying the particular values of the parameters $a, b$ and $c$.

In a standard computer programming language, we can write *functions* that encapsulate the solutions of the equation, but calling those functions requires us to specify values of the parameters. In general, the value of a variable must be given before the variable can be used.

However, there *do* exist *Computer Algebra Systems* that can perform manipulations in the "standard" mathematical form. Through the university you will have access to Wolfram Mathematica and Maple, which are commercial packages providing a huge range of mathematical tools. There are also freely available packages, such as SageMath and `sympy`. These are not always easy to use, as all CAS have their own formal languages that rarely perfectly match your expectations.

Here we will briefly look at `sympy`, which is a pure Python CAS. `sympy` is not suitable for complex calculations, as it's far slower than the alternatives. However, it does interface very cleanly with Python, so can be used inside Python code, especially to avoid entering lengthy expressions.

# sympy

## Setting up

Setting up `sympy` is straightforward:



{:.input_area}
```python
import sympy
sympy.init_printing()
```


The standard `import` command is used. The `init_printing` command looks at your system to find the clearest way of displaying the output; this isn't necessary, but is helpful for understanding the results.

To do *anything* in `sympy` we have to explicitly tell it if something is a variable, and what name it has. There are two commands that do this. To declare a single variable, use



{:.input_area}
```python
x = sympy.Symbol('x')
```


To declare multiple variables at once, use



{:.input_area}
```python
y, z0 = sympy.symbols(('y', 'z_0'))
```


Note that the "name" of the variable does not need to match the symbol with which it is displayed. We have used this with `z0` above:



{:.input_area}
```python
z0
```





$$z_{0}$$



Once we have variables, we can define new variables by operating on old ones:



{:.input_area}
```python
a = x + y
b = y * z0
print("a={}. b={}.".format(a, b))
```


{:.output .output_stream}
```
a=x + y. b=y*z_0.

```



{:.input_area}
```python
a
```





$$x + y$$



In addition to variables, we can also define general functions. There is only one option for this:



{:.input_area}
```python
f = sympy.Function('f')
```


## In-built functions

We have seen already that mathematical functions can be found in different packages. For example, the $\sin$ function appears in `math` as `math.sin`, acting on a single number. It also appears in `numpy` as `numpy.sin`, where it can act on vectors and arrays in one go. `sympy` re-implements many mathematical functions, for example as `sympy.sin`, which can act on abstract (`sympy`) variables.

Whenever using `sympy` we should use `sympy` functions, as these can be manipulated and simplified. For example:



{:.input_area}
```python
c = sympy.sin(x)**2 + sympy.cos(x)**2
```




{:.input_area}
```python
c
```





$$\sin^{2}{\left (x \right )} + \cos^{2}{\left (x \right )}$$





{:.input_area}
```python
c.simplify()
```





$$1$$



Note the steps taken here. `c` is an object, something that `sympy` has created. Once created it can be manipulated and simplified, using the methods on the object. It is useful to use tab completion to look at the available commands. For example,



{:.input_area}
```python
d = sympy.cosh(x)**2 - sympy.sinh(x)**2
```


Now type `d.` and then tab, to inspect all the available methods. As before, we could do



{:.input_area}
```python
d.simplify()
```





$$1$$



but there are many other options.

## Solving equations

Let us go back to our quadratic equation and check the solution. To define an *equation* we use the `sympy.Eq` function:



{:.input_area}
```python
a, b, c, x = sympy.symbols(('a', 'b', 'c', 'x'))
quadratic_equation = sympy.Eq(a*x**2+b*x+c, 0)
sympy.solve(quadratic_equation)
```





$$\left [ \left \{ a : - \frac{1}{x^{2}} \left(b x + c\right)\right \}\right ]$$



What happened here? `sympy` is not smart enough to know that we wanted to solve for `x`! Instead, it solved for the first variable it encountered. Let us try again:



{:.input_area}
```python
sympy.solve(quadratic_equation, x)
```





$$\left [ \frac{1}{2 a} \left(- b + \sqrt{- 4 a c + b^{2}}\right), \quad - \frac{1}{2 a} \left(b + \sqrt{- 4 a c + b^{2}}\right)\right ]$$



This is our expectation: multiple solutions, returned as a list. We can access and manipulate these results:



{:.input_area}
```python
roots = sympy.solve(quadratic_equation, x)
xplus, xminus = sympy.symbols(('x_{+}', 'x_{-}'))
xplus = roots[0]
xminus = roots[1]
```


We can substitute in specific values for the parameters to find solutions:



{:.input_area}
```python
xplus_solution = xplus.subs([(a,1), (b,2), (c,3)])
xplus_solution
```





$$-1 + \sqrt{2} i$$



We have a list of substitutions. Each substitution is given by a tuple, containing the variable to be replaced, and the expression replacing it. We do not have to substitute in numbers, as here, but could use other variables:



{:.input_area}
```python
xminus_solution = xminus.subs([(b,a), (c,a+z0)])
xminus_solution
```





$$- \frac{1}{2 a} \left(a + \sqrt{a^{2} - 4 a \left(a + z_{0}\right)}\right)$$





{:.input_area}
```python
xminus_solution.simplify()
```





$$- \frac{1}{2 a} \left(a + \sqrt{- a \left(3 a + 4 z_{0}\right)}\right)$$



We can use similar syntax to solve *systems* of equations, such as

$$ \begin{aligned}  x + 2 y &= 0, \\ xy & = z_0. \end{aligned} $$



{:.input_area}
```python
eq1 = sympy.Eq(x+2*y, 0)
eq2 = sympy.Eq(x*y, z0)
sympy.solve([eq1, eq2], [x, y])
```





$$\left [ \left ( - \sqrt{2} \sqrt{- z_{0}}, \quad \frac{\sqrt{2}}{2} \sqrt{- z_{0}}\right ), \quad \left ( \sqrt{2} \sqrt{- z_{0}}, \quad - \frac{\sqrt{2}}{2} \sqrt{- z_{0}}\right )\right ]$$



## Differentiation and integration

### Differentiation

There is a standard function for differentiation, `diff`:



{:.input_area}
```python
expression = x**2*sympy.sin(sympy.log(x))
sympy.diff(expression, x)
```





$$2 x \sin{\left (\log{\left (x \right )} \right )} + x \cos{\left (\log{\left (x \right )} \right )}$$



A parameter can control how many times to differentiate:



{:.input_area}
```python
sympy.diff(expression, x, 3)
```





$$\frac{1}{x} \left(- 3 \sin{\left (\log{\left (x \right )} \right )} + \cos{\left (\log{\left (x \right )} \right )}\right)$$



Partial differentiation with respect to multiple variables can also be performed by increasing the number of arguments:



{:.input_area}
```python
expression2 = x*sympy.cos(y**2 + x)
sympy.diff(expression2, x, 2, y, 3)
```





$$4 y \left(- 2 x y^{2} \sin{\left (x + y^{2} \right )} + 3 x \cos{\left (x + y^{2} \right )} + 4 y^{2} \cos{\left (x + y^{2} \right )} + 6 \sin{\left (x + y^{2} \right )}\right)$$



There is also a function representing an *unevaluated* derivative:



{:.input_area}
```python
sympy.Derivative(expression2, x, 2, y, 3)
```





$$\frac{\partial^{5}}{\partial x^{2}\partial y^{3}} \left(x \cos{\left (x + y^{2} \right )}\right)$$



These can be useful for display, building up a calculation in stages, simplification, or when the derivative cannot be evaluated. It can be explicitly evaluated using the `doit` function:



{:.input_area}
```python
sympy.Derivative(expression2, x, 2, y, 3).doit()
```





$$4 y \left(- 2 x y^{2} \sin{\left (x + y^{2} \right )} + 3 x \cos{\left (x + y^{2} \right )} + 4 y^{2} \cos{\left (x + y^{2} \right )} + 6 \sin{\left (x + y^{2} \right )}\right)$$



### Integration

Integration uses the `integrate` function. This can calculate either definite or indefinite integrals, but will *not* include the integration constant.



{:.input_area}
```python
integrand=sympy.log(x)**2
sympy.integrate(integrand, x)
```





$$x \log^{2}{\left (x \right )} - 2 x \log{\left (x \right )} + 2 x$$





{:.input_area}
```python
sympy.integrate(integrand, (x, 1, 10))
```





$$- 20 \log{\left (10 \right )} + 18 + 10 \log^{2}{\left (10 \right )}$$



The definite integral is specified by passing a tuple, with the variable to be integrated (here `x`) and the lower and upper limits (which can be expressions).

Note that `sympy` includes an "infinity" object `oo` (two `o`'s), which can be used in the limits of integration:



{:.input_area}
```python
sympy.integrate(sympy.exp(-x), (x, 0, sympy.oo))
```





$$1$$



Multiple integration for higher dimensional integrals can be performed:



{:.input_area}
```python
sympy.integrate(sympy.exp(-(x+y))*sympy.cos(x)*sympy.sin(y), x, y)
```





$$- \frac{e^{- x}}{4} e^{- y} \sin{\left (x \right )} \sin{\left (y \right )} - \frac{e^{- x}}{4} e^{- y} \sin{\left (x \right )} \cos{\left (y \right )} + \frac{e^{- x}}{4} e^{- y} \sin{\left (y \right )} \cos{\left (x \right )} + \frac{e^{- x}}{4} e^{- y} \cos{\left (x \right )} \cos{\left (y \right )}$$





{:.input_area}
```python
sympy.integrate(sympy.exp(-(x+y))*sympy.cos(x)*sympy.sin(y), 
                (x, 0, sympy.pi), (y, 0, sympy.pi))
```





$$\frac{1}{4 e^{2 \pi}} + \frac{1}{2 e^{\pi}} + \frac{1}{4}$$



Again, there is an unevaluated integral:



{:.input_area}
```python
sympy.Integral(integrand, x)
```





$$\int \log^{2}{\left (x \right )}\, dx$$





{:.input_area}
```python
sympy.Integral(integrand, (x, 1, 10))
```





$$\int_{1}^{10} \log^{2}{\left (x \right )}\, dx$$



Again, the `doit` method will explicitly evaluate the result where possible.

## Differential equations

Defining and solving differential equations uses the pattern from the previous sections. We'll use the same example problem as in the `scipy` case, 

$$  \frac{\text{d} y}{\text{d} t} = e^{-t} - y, \qquad y(0) = 1. $$

First we define that $y$ is a function, currently unknown, and $t$ is a variable.



{:.input_area}
```python
y = sympy.Function('y')
t = sympy.Symbol('t')
```


`y` is a general function, and can be a function of anything at this point (any number of variables with any name). To use it consistently, we *must* refer to it explicitly as a function of $t$ everywhere. For example,



{:.input_area}
```python
y(t)
```





$$y{\left (t \right )}$$



We then define the differential equation. `sympy.Eq` defines the equation, and `diff` differentiates:



{:.input_area}
```python
ode = sympy.Eq(y(t).diff(t), sympy.exp(-t) - y(t))
ode
```





$$\frac{d}{d t} y{\left (t \right )} = - y{\left (t \right )} + e^{- t}$$



Here we have used `diff` as a method applied to the function. As `sympy` can't differentiate $y(t)$ (as it doesn't have an explicit value), it leaves it unevaluated.

We can now use the `dsolve` function to get the solution to the ODE. The syntax is very similar to the `solve` function used above:



{:.input_area}
```python
sympy.dsolve(ode, y(t))
```





$$y{\left (t \right )} = \left(C_{1} + t\right) e^{- t}$$



This is simple enough to solve, but we'll use symbolic methods to find the constant, by setting $t = 0$ and $y(t) = y(0) = 1$.



{:.input_area}
```python
general_solution = sympy.dsolve(ode, y(t))
value = general_solution.subs([(t,0), (y(0), 1)])
value
```





$$1 = C_{1}$$



We then find the specific solution of the ODE.



{:.input_area}
```python
ode_solution = general_solution.subs([(value.rhs,value.lhs)])
ode_solution
```





$$y{\left (t \right )} = \left(t + 1\right) e^{- t}$$



## Plotting

`sympy` provides an interface to `matplotlib` so that expressions can be directly plotted. For example,



{:.input_area}
```python
%matplotlib inline
from matplotlib import rcParams
rcParams['figure.figsize']=(12,9)
```




{:.input_area}
```python
sympy.plot(sympy.sin(x));
```



{:.output .output_png}
![png](/Users/ih3/Documents/github/maths-with-python-book/_build/07-sympy_83_0.png)



We can explicitly set limits, for example



{:.input_area}
```python
sympy.plot(sympy.exp(-x)*sympy.sin(x**2), (x, 0, 1));
```



{:.output .output_png}
![png](/Users/ih3/Documents/github/maths-with-python-book/_build/07-sympy_85_0.png)



We can plot the solution to the differential equation computed above:



{:.input_area}
```python
sympy.plot(ode_solution.rhs, xlim=(0, 1), ylim=(0.7, 1.05));
```



{:.output .output_png}
![png](/Users/ih3/Documents/github/maths-with-python-book/_build/07-sympy_87_0.png)



This can be *visually* compared to the previous result. However, we would often like a more precise comparison, which requires numerically evaluating the solution to the ODE at specific points.

## lambdify

At the end of a symbolic calculation using `sympy` we will have a result that is often long and complex, and that is needed in another part of another code. We could type the appropriate expression in by hand, but this is tedious and error prone. A better way is to make the computer do it.

The example we use here is the solution to the ODE above. We have solved it symbolically, and the result is straightforward. We can also solve it numerically using `scipy`. We want to compare the two.

First, let us compute the `scipy` numerical result:



{:.input_area}
```python
from numpy import exp
from scipy.integrate import odeint
import numpy

def dydt(y, t):
    """
    Defining the ODE dy/dt = e^{-t} - y.
    
    Parameters
    ----------
    
    y : real
        The value of y at time t (the current numerical approximation)
    t : real
        The current time t
        
    Returns
    -------
    
    dydt : real
        The RHS function defining the ODE.
    """
    
    return exp(-t) - y

t_scipy = numpy.linspace(0.0, 1.0)
y0 = [1.0]

y_scipy = odeint(dydt, y0, t_scipy)
```


We want to evaluate our `sympy` solution at the same points as our `scipy` solution, in order to do a direct comparison. In order to do that, we want to construct a function that computes our `sympy` solution, without typing it in. That is what `lambdify` is for: it creates a function from a sympy expression.

First let us get the expression explicitly:



{:.input_area}
```python
ode_expression = ode_solution.rhs
ode_expression
```





$$\left(t + 1\right) e^{- t}$$



Then we construct the function using `lambdify`:



{:.input_area}
```python
from sympy.utilities.lambdify import lambdify

ode_function = lambdify((t,), ode_expression, modules='numpy')
```


The first argument to `lambdify` is a tuple containing the arguments of the function to be created. In this case that's just `t`, the time(s) at which we want to evaluate the expression. The second argument to `lambdify` is the expression that we want converted into a function. The third argument, which is optional, tells `lambdify` that where possible it should use `numpy` functions. This means that we call the function using `numpy` arrays, it will calculate using `numpy` array expressions, doing the whole calculation in a single call.

We now have a function that we can directly call:



{:.input_area}
```python
print("sympy solution at t=0: {}".format(ode_function(0.0)))
print("sympy solution at t=0.5: {}".format(ode_function(0.5)))
```


{:.output .output_stream}
```
sympy solution at t=0: 1.0
sympy solution at t=0.5: 0.9097959895689501

```

And we can directly apply this function to the times at which the `scipy` solution is constructed, for comparison:



{:.input_area}
```python
y_sympy = ode_function(t_scipy)
```


Now we can use `matplotlib` to plot both on the same figure:



{:.input_area}
```python
from matplotlib import pyplot
pyplot.plot(t_scipy, y_scipy[:,0], 'b-', label='scipy')
pyplot.plot(t_scipy, y_sympy, 'k--', label='sympy')
pyplot.xlabel(r'$t$')
pyplot.ylabel(r'$y$')
pyplot.legend(loc='upper right')
pyplot.show()
```



{:.output .output_png}
![png](/Users/ih3/Documents/github/maths-with-python-book/_build/07-sympy_101_0.png)



We see good visual agreement everywhere. But how accurate is it?

Now that we have `numpy` arrays explicitly containing the solutions, we can manipulate these to see the differences between solutions:



{:.input_area}
```python
pyplot.semilogy(t_scipy, numpy.abs(y_scipy[:,0]-y_sympy))
pyplot.xlabel(r'$t$')
pyplot.ylabel('Difference in solutions');
```



{:.output .output_png}
![png](/Users/ih3/Documents/github/maths-with-python-book/_build/07-sympy_103_0.png)



The accuracy is around $10^{-8}$ everywhere - by modifying the accuracy of the `scipy` solver this can be made more accurate (if needed) or less (if the calculation takes too long and high accuracy is not required).

# Further reading

`sympy` has [detailed documentation](http://docs.sympy.org/latest/index.html) and a [useful tutorial](http://docs.sympy.org/dev/tutorial/index.html).

# Exercise : systematic ODE solving

We are interested in the solution of

$$  \frac{\text{d} y}{\text{d} t} = e^{-t} - y^n, \qquad y(0) = 1, $$

where $n > 1$ is an integer. The "minor" change from the above examples mean that `sympy` can only give the solution as a power series.

## Exercise 1

Compute the general solution as a power series for $n = 2$.

## Exercise 2

Investigate the help for the `dsolve` function to straightforwardly impose the initial condition $y(0) = 1$ using the `ics` argument. Using this, compute the specific solutions that satisfy the ODE for $n = 2, \dots, 10$.

## Exercise 3

Using the `removeO` command, plot each of these solutions for $t \in [0, 1]$.
