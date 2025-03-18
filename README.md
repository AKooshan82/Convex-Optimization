# Conjugate Gradient Methods for Hessian-Free Optimization

## Overview

This project provides an in-depth review of **Conjugate Gradient (CG) Methods** and their application in **Hessian-Free Optimization**. These methods are particularly useful for large-scale optimization problems where traditional methods, like gradient descent or Newton's method, become inefficient due to high computational cost or issues with curvature. The focus is on Hessian-Free (HF) optimization, which uses CG methods to optimize quadratic objectives efficiently.

## Key Concepts

### 1. **Newton's Method**
Newton's method uses second-order optimization to approximate an objective function. The approximation is done using the quadratic function:
   
  $$
   f(\theta + \alpha \cdot p) \approx f(\theta) + \nabla f(\theta)^T p + \frac{1}{2} p^T B p
  $$

   where \( $B$ = $H(\theta)$ \) is the Hessian, and \( $p$ \) represents the search direction. However, for large models, computing the Hessian matrix becomes computationally expensive, and the method may fail due to issues like an indefinite Hessian.

### 2. **Hessian-Free Optimization**
The Hessian-Free method avoids explicit computation of the Hessian matrix, which can be prohibitive for large models. It approximates the Hessian-vector product efficiently using finite differences:

   $$
   H d = \lim_{\epsilon \to 0} \frac{\nabla f(\theta + \epsilon d) - \nabla f(\theta)}{\epsilon}
   $$

The method leverages **Conjugate Gradient** (CG) to minimize quadratic objectives and obtain an efficient update for the optimization process.

### 3. **Conjugate Gradient Method**
The Linear Conjugate Gradient method solves the system of linear equations \( $Ax = b$ \), minimizing the quadratic function:

   $$
   f(x) = \frac{1}{2} x^T A x - b^T x + c
   $$

   The algorithm iteratively updates the solution estimate, moving along conjugate directions:

   1. **Initialization**: Start with an initial guess for \( $x$ \), and calculate the residual \( $r_0 = b - A x_0$ \).
   2. **Iterative Update**: Compute the step length \( $\alpha_k$\), update the solution \($x_{k+1} = x_k + \alpha_k p_k$\), and compute the new residual and direction.
   3. **Termination**: The algorithm stops when the residual is sufficiently small, indicating convergence.

#### Conjugate Gradient Update Formula:
The step size \( $\alpha_k $\) is computed as:
   
   $$
   \alpha_k = \frac{r_k^T r_k}{p_k^T A p_k}
   $$

   The search direction \( $p_{k+1} $\) is updated as:
   
   $$
   p_{k+1} = r_{k+1} + \beta_k p_k
   $$
   
   with \( $\beta_k = \frac{r_{k+1}^T r_{k+1}}{r_k^T r_k}$ \).

### 4. **Nonlinear Conjugate Gradient: Fletcher-Reeves Algorithm**
This method extends CG to nonlinear functions, iteratively minimizing a nonlinear objective \( $f(x)$ \) by adjusting the search directions using the Fletcher-Reeves parameter.

   $$
   d_k = - \nabla f(x_k) + \beta_k d_{k-1}
   $$

   where \( $\beta_k$ \) is computed as:

   $$
   \beta_k = \frac{\nabla f(x_k)^T \nabla f(x_k)}{\nabla f(x_{k-1})^T \nabla f(x_{k-1})}
   $$

   This ensures conjugacy between directions and leads to faster convergence.

## Practical Applications and Results

- **Linear Conjugate Gradient**:
  The Conjugate Gradient method is highly efficient for large systems and often requires fewer iterations than traditional methods such as Steepest Descent. For example, for a 100x100 matrix, the Conjugate Gradient method converges in approximately 50 iterations, whereas Steepest Descent requires about 500 iterations.

- **Comparison with Steepest Descent**:
  The Conjugate Gradient method is significantly more efficient than Steepest Descent, particularly in large-scale problems where Steepest Descent struggles due to slow convergence along poorly conditioned directions.

## Conclusion

Conjugate Gradient methods provide a powerful tool for solving large linear systems and optimizing quadratic functions. By using conjugate directions and avoiding the direct computation of the Hessian, these methods improve efficiency and scalability, especially in large models such as neural networks.

## Installation and Implementation

The implementation of the Conjugate Gradient method and other algorithms discussed in this project is available in the provided Jupyter notebook. 
