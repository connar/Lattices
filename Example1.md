# Example 1 - Simple use of lattice to recover some variables that are unknown but exist in some equation

Assume the following problem:
```
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
h = (inverse(f, q)*g) % q  
$ \Leftrightarrow $ h * $ f^-1 $

