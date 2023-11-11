# Lattices
My notes on lattices for ctfs and understand in general:)


# What is a Lattice?
Lattice is the number of all linear combinations that can solve a problem based on a given Matrix base.

# What is a Matrix base?
Assume the following Matrix:  
![image](https://github.com/connar/Lattices/assets/87579399/1a6d90bb-4876-4c94-839e-58fd48e14528)

The vectors [a, 1] and [w, j] are basically the base of the Matrix.
To solve problems using Matrixes, we want to make a specific Matrix base from some vectors we will choose, in order for the LLL algorithm (which we will see shortly) to return the smallest linear combination.

# Why we use Matrixes to solve math problems?
Matrixes try to solve some linear equation, for example: x = 5y + 13w --> find (x, y, w)
Matrixes, given a correct base (i.e. choosing some vectors to be the base of the Matrix), try to solve an equation by finding a solution vector, where a solution vector is just one of the MANY linear combinations that solve the same problem. So how do we know what we are searching for?

# LLL
Using the LLL algorithm, we try to solve the given equation problem by making an ideal Matrix. The LLL algorithm will then try and solve this problem. What the LLL will return will be (if we are lucky) the shortest vector that solves the problem. This is better known as SVP (Shortest Vector Problem).

Based on what unknown variables we want to reveal (find out), we make adjustments to the Matrix that we will give to LLL so the result that the LLL will return us will contain the variables we were searching for.

In other words, what is basically happening is that in the lattice that the given base vectors form, many solutions exist within it. Imagine like we construct a box in the 3D space, and within that box there are many vectors (lines) that solve a problem. Usually, we try to find the shortest vector that solves our problem.

