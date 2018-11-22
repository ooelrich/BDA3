BDA3 Exercises: 1
================
Oscar Oelrich
11 november 2018

Suggested solutions to some of the exercises in Bayesian Data Analysis 3rd edition by Gelman et al.

Chapter 1
=========

Exercise 1.1
------------

### Part a

Since *θ* is a discrete variable which takes only the values 1 and 2, the marginal probability density for *y* will be obtained by summing over *θ*

$$\\begin{equation}
p(y) = \\sum\_{i=1}^2 p(y|\\theta\_i) p(\\theta\_i) = \\frac{1}{2}p\_1(y)+\\frac{1}{2}p\_1(y)
\\end{equation}$$

where *p*<sub>1</sub>(*y*) is normal with mean 1 and standard deviation *σ* and *p*<sub>2</sub>(*y*) is normal with mean 2 and standard deviation *σ*. Using *σ* = 2 the density will be given by

$$\\begin{equation}
p(y)=\\frac{1}{2} \\frac{1}{\\sqrt{2\\pi 2^2}}e^{-(y-1)^2/(2\*2^2)}   + \\frac{1}{2}\\frac{1}{\\sqrt{2\\pi 2^2}}e^{-(y-2)^2/(2\*2^2)}= \\frac{1}{4\\sqrt{2\\pi}}\\left(e^{-(y-1)^2/(2\*2^2)}+e^{-(y-2)^2/(2\*2^2)}\\right)
\\end{equation}$$

We plot the density

``` r
p1 <- function(y) 0.25*(1/sqrt(2*pi))*(exp(-(y-1)^2/(2*2^2))+exp(-(y-2)^2/(2*2^2)))
# Or we could just use the build in densities from r...
#p2 <- function(y) 0.5*dnorm(y, 1, 2)+0.5*dnorm(y,2,2)
x <- seq(-5, 8, 0.001)
plot(x, p1(x), type = 'l')
```

![](bda3-exercises-1_files/figure-markdown_github/unnamed-chunk-1-1.png)

### Part b

Using Bayes' theorem we have that

$$\\begin{equation}
p(\\theta=1|y=1) = \\frac{p(y=1|\\theta=1) p(\\theta=1)}{p(y=1)}
\\end{equation}$$

which we calculate to be

``` r
dnorm(1,1,2)*0.5/(0.5*dnorm(1, 1, 2)+0.5*dnorm(1,2,2))
```

    ## [1] 0.5312094

That is, after having observed *y* = 1 we update our believes favouring *θ* = 1, but not by much.

### Part c

Given that we have observed *y* = 1, decreasing the value of the variance means that the observation becomes less and less probable under the alternative *θ* = 2 and so the posterior will put more and more weight on *θ* = 1 as the variance decreases. As the variance increases, the probabilities under the two values will creep closer to each other and the posterior will get closer to the prior of $\\frac{1}{2}$.
