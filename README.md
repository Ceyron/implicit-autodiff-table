# Implicit Autodiff Table 📚

A collection of advanced autodiff primitive rules that built upon the implicit
function theorem both for discrete problems (like solving linear systems of
equations) and (semi-)continuous problems (like ordinary/partial differential
equations).

👉 Find the web version here: [ceyron.github.io/implicit-autodiff-table/](https://ceyron.github.io/implicit-autodiff-table/)

(the section on partial differential equations is a work in progress)

### 💡 Background

Automatic differentiation is a transformation of the computational graph
associated with the algorithmic implementation of a mathematical function. It
breaks it down into atomistic primitive operations for which symbolic
derivatives are available. This can be on the scalar level or the matrix/vector
level. The latter is typical for modern autodiff engines that power deep
learning, like TensorFlow, PyTorch, JAX, etc. See
[this](https://github.com/Ceyron/autodiff-table) repository for a collection of
these explicit rules.

Going beyond classical feed-forard deep learning architectures, one commonly
finds that problems are expressed as the solution to implicit relations. For
example, many simulations in scientific computing boil down to the solutions of
linear systems of equations. Similarly like we can break up a matrix-vector
multiplication into individual scalar operations, we could break down the linear
solve into its algorithmic components. This comes with several disadvantages
like long tapes needed for the reverse-mode and potential numerical
instabilities. Based on the implicit function theorem, one can devise (rather
abstract) auxiliary operations that behave (somehow) equivalent as if we had
opened up the black box. This repository aims to be a collection of those.

For example, if our primal problem was to solve a linear system of equations for
$x$

$$Ax = b,$$

then the forward propagation would first compute the auxiliary vector

$$d = \dot{b} - A \dot{x}$$

and then solve the tangent linear system for $\dot{x}$

$$A \dot{x} = d.$$

For the reverse propagation, we would first solve the adjoint linear system for
$\lambda$

$$A^T \lambda = \bar{x}.$$

Then, we find the backpropagated cotangent information on right-hand side and
system matrix as

$$\bar{b} = \lambda,$$
$$\bar{A} = -\lambda \dot{x}^T.$$

### 𓊍 Even more levels

When it comes to the solution of differential equations, we also have the option
to find propagation rules on the continuous level. This gives rise to the famous
*adjoint method* that was popularized by the [Neural ODE
paper](https://arxiv.org/abs/1806.07366). However, continuous adjoint methods
existed for a long time before that, motivated by tasks in optimal control.
Indeed, the history of automatic differentiation was greatly influenced by them (see the [history section](https://en.wikipedia.org/wiki/Backpropagation#History) of the Wikipedia article on backpropagation).

### 🏦 References

todo: have this more scientifical and extend

* A classical write-up is by [Andrew Bradley](https://cs.stanford.edu/~ambrad/adjoint_tutorial.pdf)
* I also liked this [first](https://math.mit.edu/~stevenj/18.336/adjoint.pdf) and [second](https://math.mit.edu/~stevenj/18.336/recurrence2.pdf) pdf by Prof. Steven Johnson.
* Rules for Ordinary Differential Equations:
    * I liked the derivations in [Sengupta et al.](https://www.sciencedirect.com/science/article/pii/S1053811914003097).