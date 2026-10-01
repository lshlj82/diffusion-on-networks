# Diffusion on networks

An interactive, single-page demo of spreading and diffusion on networks, built around the adjacency matrix $\mathbf{A}$ and the Laplacian matrix $\mathbf{L} = \mathbf{D} - \mathbf{A}$.

Made by Claude Opus 5.5, an AI model by Anthropic. The content follows Sang Hoon Lee's lecture slides on the adjacency matrix, the Laplacian matrix, and spreading dynamics.

## What's inside

The page has three parts. They all use the same network, which you pick from the menu at the top.

**1. Spreading with the adjacency matrix.** Step through $\mathbf{v}_{n+1} = \mathbf{A}\mathbf{v}_n$ one multiplication at a time. The page shows the matrix, the current vector, and the result. You can watch the total grow, because a node with $k$ edges multiplies what it holds by $k$. On bipartite networks the quantity sloshes back and forth between the two sides. You can also rescale after each step so the total stays at 1.

**2. Diffusion with the Laplacian.** This runs the continuous dynamics $d\mathbf{v}/dt = -c\mathbf{L}\mathbf{v}$.
- Choose how the run starts: everything on one node, the same amount everywhere, random amounts, uniform plus the slowest ripple, or values you type in.
- The full system of equations is shown, one line per node, using the color-boxed notation from the slides. Blue boxes are the degree term and red boxes are the neighbor term, and each line shows its current rate of change.
- A time-series plot shows every node's value and the steady-state level.
- A sign switch compares $-\mathbf{L}$ with $+\mathbf{L}$, which is the sign written on the slides.

**3. Eigenmodes.** Each eigenvector of $\mathbf{L}$ gets a row with a thumbnail of its pattern on the network. A slider sets how much of that mode is in the starting state, and a checkbox includes or leaves out the mode. Drag the time slider or press Play to watch the solution $\mathbf{v}(t) = \sum_i c_i e^{-\lambda_i t} \mathbf{x}_i$ evolve. The network, the live formula, and the decay curves all update together. Buttons let you load part 2's starting state, make a random mix, or keep only the steady state.

These networks are included:
- the 3-node and 4-node examples from the slides
- a path
- a star
- a ring
- two clusters joined by one edge, which has a small $\lambda_2$ and mixes slowly
- two separate triangles, which have two zero eigenvalues
- a random graph

## A note on the sign

The slides write $d\mathbf{v}/dt = \mathbf{L}\mathbf{v}$. Because every eigenvalue of $\mathbf{L}$ is $\geq 0$, that version makes non-uniform patterns grow exponentially. In the slides' general solution, that is the $\lambda > 0$ \"growing solution\" case. Physical diffusion, where the quantity flows from high to low, is $d\mathbf{v}/dt = -\mathbf{L}\mathbf{v}$, and the demo uses that by default. Both versions conserve the total, and both have the uniform vector $\mathbf{v}_{st}$ as a steady state. The sign switch in part 2 lets you compare them.

## Running it

It's one self-contained HTML file with no build step and no dependencies.

- **Locally:** open `index.html` in any modern browser.
- **GitHub Pages:** push this folder to a repository. Then go to *Settings → Pages* and choose to deploy from the branch that contains `index.html`. The demo will be served at `https://<user>.github.io/<repo>/`.

The only external requests are for the Kalam and Source Serif 4 web fonts from Google Fonts. Without a network connection, the page falls back to system fonts and still works fully.

## How it works

- Eigenvalues and eigenvectors of $\mathbf{L}$ are computed in the browser with the Jacobi method for symmetric matrices.
- Part 2 integrates the ODE with fourth-order Runge–Kutta, using a step size of 0.005.
- Part 3 uses the exact solution from the eigen-decomposition, so its time slider can jump to any time instantly.
- The page follows your system's light or dark setting.

## Credits

- Made by Claude Opus 5.5 (Anthropic).
- Based on Sang Hoon Lee's lecture slides on the adjacency matrix, the Laplacian matrix, and spreading dynamics.
