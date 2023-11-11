# Example 2 - A looking into the Hidden Number Problem (HNP) and the Embedding method

# HNP
Assume the following code:
```py
...
r = random.randint(2, int(math.sqrt(q // 2)))
e = (r*h + m) % q
return e
```

Also, assume that h and q are known. How do we find m?
We can rewrite the equation of 'e' as:  
e = (r*h + m) % q  
$\Leftrightarrow$ e - r*h $\equiv$ m + k*q
$\Leftrightarrow$ m = e - r*h - k*q

We can construct a lattice basis like the following one:  
![image](https://github.com/connar/Lattices/assets/87579399/5cc61f12-05b8-4e28-a880-a4228e7782f8)



where B is an upper bound for m such that m <= B <= q.
We are targeting a short vector (m, Br, B), which belongs to the lattice we constructed since:  
![image](https://github.com/connar/Lattices/assets/87579399/c95cbdf9-64e9-4269-bf47-ca21a26d924f)



This is also a form of Embedding method, since the vector that we will get as a solution contains the unknown 'r' factor:  
![image](https://github.com/connar/Lattices/assets/87579399/216b1181-0dfc-44c9-9013-cb652fce13b4)

So a lot of times, we might care about the other unknowns, not just recovering a message. In that case, we form a base lattice according to an embedding method (putting extra lines and columns in our base lattice to get more information back in the solution vector after LLL).
