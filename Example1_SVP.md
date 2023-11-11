# Example 1 - Simple use of lattice to recover some variables that are unknown but exist in some equation

Assume the following problem:
```py
def gen_key():
    q = getPrime(512)
    upper_bound = int(math.sqrt(q // 2))
    lower_bound = int(math.sqrt(q // 4))
    f = random.randint(2, upper_bound)
    while True:
        g = random.randint(lower_bound, upper_bound)
        if math.gcd(f, g) == 1:
            break
    h = (inverse(f, q)*g) % q
    return (q, h), (f, g)

public, private = gen_key()
q, h = public
f, g = private
...
...
...
```

Don't get absorbed by what the upper_bound, lower_bound etc are. Just observe the following lines of the code that are important:
```py
h = (inverse(f, q)*g) % q
return (q, h), (f, g)
```

Assume that only (q,h) are known to us and we want to recover (f,g) which is the private key. How are we going to do that?
Well, one easy way to recover them is by using lattices. How?
Observe the equation:  
h = (inverse(f, q) * g) % q  
$\Leftrightarrow$ h * f $\equiv$ g % q  
$\Leftrightarrow$ h * f $\equiv$ g + k * q  
$\Leftrightarrow$ h * f - k * q $\equiv$ g   

So we have g $\equiv$ h * f - k * q  (1). Note that ```inverse(f, q)``` is basically just the inverse of f mod q, thats why we multiplied with f - to just get rid of its inverse.
From that equation, we only know q and h, but we don't know k, f and g. So it seems its a not solvable problem, but with lattices we can recover the (f, g) vector.

To do so, we need to construct a base for matrix and then pass it to LLL. How is LLL going to find the correct vector solution will be explained later.
The lattices are so powerful because we can create whatever base we want. Here, we can rewrite the right part of the equation (1) as a multiplication of the following vectors:  
![image](https://github.com/connar/Lattices/assets/87579399/f3e95d98-cc01-4342-b6e5-a05b88ae08e2)


This - making the multiplication between the vectors - would return the equation (1): h * f - k * q. So if we were to pass the matrix [[h, 0],[-q,0]], we would get g. But what about f? How can we get f? Well, since we decide what base matrix to give to LLL, we could pass [-q, 1] instead of [-q, 0], resulting in the following:

![image](https://github.com/connar/Lattices/assets/87579399/85707428-e8f3-44de-a790-ce43f5ec64eb)

So if we had given the matrix [[h, 1],[-q,0]] to LLL, we would get a solution vector which would be (g, f) - All that because we made the correct base matrix!



To align what we just read with the README.md theory, we have:
- base vectors: [h, 1] and [-q, 0]
- One of the many linear combinations that is a solution to our matrix problem is the [g, f]. This happens to be the shortest one and is found by LLL algorithm which tries to solve the problem and returns the smallest solution (the smallest linear combination vector).

A question that might arise is: *what can we do to find the -k variable?*
This is also a common problem in problems like lattices for example, and is solved by the embedding method (see README.md for the theory)
