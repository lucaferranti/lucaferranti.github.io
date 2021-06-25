+++
title = "Hello IntervalLinearAlgebra.jl"
pubdate = Date("2021-06-25")
img = "/posts/2021/06/figures/logo.png"
+++

Hello everyone and welcome to the first blog of my GSOC'21 project. Here I will give a
short project overview and present the first results I have obtained so far.

## Project overview

The purpose of the project is to develop [IntervalLinearAlgebra.jl](https://github.com/lucaferranti/IntervalLinearAlgebra.jl)
a package to perform numerical linear algebra _rigorously_, i.e. using interval arithmetic.
The package is fully written in [Julia](https://julialang.org/) and is built on top of [IntervalArithmetic.jl](https://github.com/juliaIntervals/IntervalArithmetic.jl) for interval computations.

## Basic concepts

As we are working with interval arithmetic, the most fundamental mathematical structure is _interval_.
An interval $[a, b]$ is defined as a subset of $\mathbb{R}$ as follows

$$
[a, b] = \{x \in \mathbb{R} | a \le x \le b \}
$$

Next, we introduce the concept of _interval matrix_, that is a matrix whose entries are intervals.
More formally, let us denote by $\mathbb{I}\mathbb{R}$ the set of real intervals. Then an interval
matrix $\mathbf{A}\in\mathbb{I}\mathbb{R}^{m\times n}$ is defined as

$$
\mathbf{A} = \{ A \in \mathbb{R}^{m\times n} | A_{ij} \in \mathbf{A}_{ij}, 1\le i \le m, 1\le j \le n\}
$$

Hence an interval matrix can be thought as a set of real matrices. Let us give an example

$$
\mathbf{A} = \begin{bmatrix}
[2, 4]&[-2,1]\\
[-1, 2]&[2, 4]
\end{bmatrix}
$$

is an interval matrix and for example

$$
A_1=\begin{bmatrix}
2&0\\
1.5&3
\end{bmatrix} \in \mathbf{A}
$$

but

$$
A_1=\begin{bmatrix}
2&0\\
1.5&8
\end{bmatrix} \notin \mathbf{A}
$$

## Interval linear systems

At the moment, the functionalities of the package are limited to solve square interval systems,
that is systems in the form

$$
\mathbf{A}\mathbf{x}=\mathbf{b}
$$

where $\mathbf{A}\in\mathbb{I}\mathbb{R}^{n\times n}$ and $\mathbf{b}\in\mathbb{I}\mathbb{R}^n$.

Now it's legittimate to ask the question: what does it mean to solve an interval linear system, in other words, what is $\mathbf{x}$? It is
defined as

$$
\mathbf{x} = \{x \in \mathbb{R}^n | Ax=b \text{ for some } A\in\mathbf{A}, b\in\mathbf{b} \}
$$

in other words $x$ is the set of solutions of the real linear systems $Ax=b$ for which $ A\in\mathbf{A}$ and $b\in\mathbf{b}$.
Again, the interval linear system can be thought as a set of real linear systems. 
The solution of the interval linear system is the set of solutions of the real linear systems in the interval system.

## Characterizing the solution of an interval linear system

We now know what an interval linear system is and what solving it means. But how do we solve it? A naive approach would be to use
Montecarlo, i.e. to randomly sample elements from the intervals and solve the several random real systems.
Hopefully, repeating several times, we will get a good approximation of the true solution. Let us try it.
Suppose we want to solve the linear system

$$
\begin{bmatrix}
[2, 4]&[-2,1]\\
[-1, 2]&[2, 4]
\end{bmatrix}\mathbf{x} =
\begin{bmatrix}
[-2, 2]\\
[-2, 2]
\end{bmatrix}
$$

first let us import `IntervalArithmetic.jl` to define the matrix and vector.

```julia
using IntervalArithmetic

A = [2..4 -2..1; -1..2 2..4]
b = [-2..2, -2..2]
@show A, b
```

```
(A, b) = (Interval{Float64}[[2, 4] [-2, 1]; [-1, 2] [2, 4]], Interval{Float
64}[[-2, 2], [-2, 2]])
(Interval{Float64}[[2, 4] [-2, 1]; [-1, 2] [2, 4]], Interval{Float64}[[-2, 
2], [-2, 2]])
```





Now we need a function to sample from an intervals

```julia
sample(x) = rand()*(sup(x) - inf(x)) + inf(x)
```

```
sample (generic function with 1 method)
```





we are now ready for our montecarlo simulation, let us solve $100000$ random instances

```julia
N = 100000

xs = [sample.(A)\sample.(b) for _ in 1:N]
```

```
100000-element Vector{Vector{Float64}}:
 [0.3675588743168303, 0.28164434880716016]
 [-0.16532451692481342, -0.14094324290017501]
 [-0.49430847122193655, -0.34028913779324355]
 [0.49587754910595727, -0.06771426545272717]
 [0.26928278788575294, -0.7190682638766965]
 [0.5231931726314687, -0.4843086454609057]
 [0.6198610291052782, -0.20380178164383136]
 [-0.10539770299004424, 0.5371501041198676]
 [0.811761821912226, 0.4442893649050811]
 [0.2784681968502335, 0.54703603897014]
 ⋮
 [-0.1550285530472463, -0.12110935725403765]
 [-0.39791200107041474, 0.4930013023034729]
 [0.5361702873438308, 0.5205224155092559]
 [-0.010689597217576756, 0.7866615006899088]
 [0.8207604054068416, 0.4611005234633163]
 [0.025012938922391776, -0.689159868674039]
 [-0.8388763270895144, 0.6263685003924494]
 [-0.018497350801918916, -0.3739913473763062]
 [0.052494370273044044, -0.8244398045111828]
```





and let's plot the solution

```julia
using Plots

x = [xs[i][1] for i in 1:N]
y = [xs[i][2] for i in 1:N]

scatter(x, y, leg=false, ratio=1, alpha=0.5)
```

![](/posts/2021/06/figures/gsoc_blog1_4_1.png)



Looks a little messy, let us plot  2D-histogram instead
```julia
histogram2d(x, y)
```

![](/posts/2021/06/figures/gsoc_blog1_5_1.png)



as we can see, most of the solutions seem to be condensed close to the origin, but repeating the
experiments enough times we also got some solutions farther away, obtaining a star looking area.
Now the question is, do we have the whole star?


Before we answer the question, we need to recall a couple of concepts from interval arithmetic. 
Given an interval $X = [a, b]$, we define:
- the *center* $mid(X) = \frac{a+b}{2}$
- the *radius* $rad(X) = \frac{b-a}{2}$

let us also denote
- the *center matrix* $A_c = mid(A)$
- the *radius matrix* $A_\Delta = rad(A)$

where the operations `mid` and `rad` are applied to the matrices elementwise.

We are now ready to state the *Oettli-Präger* theorem, which says that an interval linear system $\mathbf{A}\mathbf{x}=\mathbf{b}$
is equivalent to the set of real inequalities

$$
|A_cx-b_c| \le A_\Delta|x| + b_\Delta,
$$
where the absolute values are to be taken elementwise.

We have now transformed the set of interval equalities into a set of real inequalities.
How to find the set of points satisfying those inequalities? [IntervalConstraintProgramming.jl](https://github.com/JuliaIntervals/IntervalConstraintProgramming.jl) comes to the rescue!

So to solve the interval linear system we should
- write the inequalities using Oettli-Präger
- solving the inequalities using `IntervalConstraintProgramming.jl`

`IntevalLinearAlgebra.jl` has a function that does all of this for you! Let's import it, note we also need to import `IntervalConstraintProgramming.jl`

```julia
using IntervalLinearAlgebra, IntervalConstraintProgramming
```




then we need an initial enclosure of the solution. We will discuss later how to find this,
for now, let us just cheat and rabbit out a good initial guess

```julia
X = IntervalBox(-5..5, 2)
```

```
[-5, 5]²
```





at the moment, we also need to provide a list of variables, this will be automated soon!

```julia
vars = (:x, :y)
```

```
(:x, :y)
```





now we can solve the interval linear system using Oettli-Präger theorem

```julia
p = oettli(A, b, X, vars)
```

```
Paving:
- tolerance ϵ = 0.01
- inner approx. of length 13712
- boundary approx. of length 7489
```





to understand what `p` is we would need to go into the specifics of `IntervalConstraintProgramming.jl`.
Let's just say that `p` has two lists of small interval boxes, one containing those boxes strictly inside the solution set and
one containing the boxes at the boundary.

Finally let us plot the solution on the same figure with the 2d-histogram

```julia
plot(p.inner, legend=false, ratio=1, lw=0)
plot!(p.boundary)
histogram2d!(x, y)
```

![](/posts/2021/06/figures/gsoc_blog1_10_1.png)



as we can see, the original montecarlo approximation, despite the high number of iterations,
was pretty disappointing.

## Conclusions

we have discussed what an interval linear system is and observed that it solution set
can have a complex non-convex shape. We also gave a theorem that can be used to characterize
the solution of the interval linear system. However, there are a couple of open entry_point_and_project_file_inside

- how do we find the starting enclosure?
- Oettli-Präger becomes unpractical in higher dimensions

both points can be summarized into one

- how can we find a tight interval box (a vector of intervals) containing the solution of the
interval linear system?

The answer of this question will be the topic of the next blog entry. Stay tuned!