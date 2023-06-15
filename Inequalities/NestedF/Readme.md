# Proof F(a) & F(b) != F(a & F (b) )

We want to check if 

```
F(a) & F(b) <==> F(a & F (b) )
```

if this is true, then using the commutative property of logic and (&) it follows that,
```
F(a) & F(b) <==> F(b) & F(a) <==> F(b & F (a) ) 
```

We can create a simple DTMC model with states
x=0 -> x=1 -> x=2
where "a" is true in x=1 and "b" in x=2.


```
dtmc
formula a = x=1;

formula b = x=2;



module req1
 x:[0..5];
 [ ] x=0 -> (x'=1);
 [ ] x=1 -> (x'=2);

endmodule
```

In PRISM, we can test our hypothesis by checkig if there is a path ("E") (or all paths ("A")) that satisfy this properties.
If the results are different (i.e., one returns True and the other False), we prove that this two formulae are not equivalent (as if they were the same, they would give the same result, of course!).

```
E[ F( a & (F b) )]
E[ F( b & (F a) )]
```

RESULTS. The first one returns "True" and the second "False"! Hence, we can say that,
```F(a) & F(b) !== F(a & F (b) )```

because otherwise the following should be true, and we disproved it!

```
F(a & F(b) ) <==> F(a) & F(b) <==> F(b) & F(a) <==> F(b & F (a) ) 
```

# Intuitive explanation
Imagine a DTMC with a true in x2 and b true in b
```
x1 -> x2 -> x3
       b     a
```
If we say F(a & F(b))
we must check for every state starting from x1, if there is a state that "a" and "F b" holds.
In x1, "a"=false, "F b"=true, hence "a & F(b)"= false
In x2, "a"=false, "F b"=true, hence "a & F(b)" =false
In x3, "a"=true, "F b"=false, hence "a & F(b)"= false
Hence F(a & F(b)) is false as "a & F(b)" never becomes true. 

Now testing F(a) & F(b), this is evaluated in the first state x1,
In x1, "F a"=true, "F b"=true, hence "F(a) & F(b)"= true

Now we can see that F(a & F(b)) != F(a) & F(b).

