# Physics 427 Homework 5

__Due 11:59pm Monday 10/2/2023__

Now that we have a good general ODE solver, let's have some fun playing with
classical systems of differential equations. This homework is intentionally
short so that you can have spare time to work on Project 1.

## 1. The Brusselator

The Brusselator is a theoretical model for a type of autocatalytic reaction, where the product of a chemical reaction is also a catalyst for the same reaction. Using $x(t)$ and $y(t)$ to denote the chemical concentrations of two particular reactants, the following equations describe their evolution:

$$
\begin{align}
\frac{dx}{dt} &= a - (1 + b)x + x^2y \\
\frac{dy}{dt} &= bx - x^2y
\end{align}
$$

The parameters $a$ and $b$ denote the concentrations of other reactants, and are kept fixed. This set of equations is interesting from a physics point of view because the system admits a critical point $(a, b/a)$. If $b < 1 + a^2$, then the solution will be attracted to this critical point. When $b > 1 + a^2$, the critical point is unstable and the solution approaches a _limit cycle_, or a closed trajectory in $xy$ plane. The $b = 1 + a^2$ case gives an an "attracting limit cycle" where the solution asymptotes to the critical point in a series of closed cycles. The $b = 1 + a^2$ point is also called a _supercritical Hopf bifurcation_. Look it up if you are interested!

In a C++ file `problem1.cpp`, implement the above system of equations and solve them using one of the ODE solvers in Homework 4. Compute the solution for different cases, first one with $a = 1$ and $b = 1$; second one with $a = 1$, $b = 2$; and third one with $a = 1$ and $b = 3$. Start with an initial condition $x = 2, y = 0$, and integrate for a reasonably long time ($t \gtrsim 100$). Plot the two results in python and commit your plots to the repository as `problem1-b-1.png`, `problem1-b-2.png`, and `problem1-b-3.png`, corresponding to the $b = 1$, $b = 2$, and $b = 3$ cases respectively. Remember to label your axes.

Play with the initial conditions a bit and see what happens!

## 2. The Lorenz System

The Lorenz system is a famous one due to its strange attractor solution:

$$
\begin{align}
\frac{dx}{dt} &= \sigma (y - x) \\
\frac{dy}{dt} &= x (\rho - z) - y \\
\frac{dz}{dt} &= xy - \beta z
\end{align}
$$

This system of differential equations was first put forward by Lorenz in 1963 to provide a simple and idealized model of convection in a slab of fluid. The aim was to gain insight into the dynamics of weather systems. The constants $\sigma$, $\rho$, and $\beta$ are parameters related to the Prandtl number, Rayleigh number, and the dimension of the slab itself.

The most famous set of parameter values is $\sigma = 10$, $\beta = 8/3$, and $\rho = 28$. Under this set of parameters, almost all initial points will lead to a strange, fractal shape that looks like two intersecting swirls. This strange attractor is also related to a Hopf bifurcation at $\rho = 24.74$. Let's solve this system and visualize the result.

In a C++ file `problem2.cpp`, implement the system described above and solve them using one of the ODE solvers in Homework 4. Use an initial condition of your choice (except $x = y = z = 0$). Integrate the system for a reasonably long time ($t \gtrsim 200$). Write your output to a file and plot it using Python. Produce a 2D image of the trajectory by plotting $x$ vs $z$, and include the plot in the repository as `problem2.png`. Remember to label your axes!

Let's also visualize this trajectory in 3D. The following part is completely optional and does not contribute to the points for the homework, but should be quite fun. Install the package `k3d` using the following command:

``` sh
pip install k3d
```

In a Jupyter notebook, you can now plot the trajectory in an interactive 3D environment using the following code snipped:

``` python
data = np.loadtxt('lorenz.csv', delimiter=',')
x = data[:,1]
y = data[:,2]
z = data[:,3]

vertices = np.vstack([x,y,z]).T
plt_line = k3d.line(vertices, width=0.1)

plot = k3d.plot()
plot += plt_line
plot.display()
```

In the upper-right corner of the interactive window, you can find box called "K3D panel". You can click on "Controls" -> "Snapshot HTML", which will export the plot into a stand-alone html file. If you are able to carry out this, include the html file in the repository as `problem2.html`.

Feel free to play with different initial conditions, and/or different sets of coefficients $\sigma$, $\beta$, and $\rho$.

