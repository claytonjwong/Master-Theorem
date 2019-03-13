# Master Theorem
#### Determine the asymptotic bound of recursive algorithms via standard recurrences
* [What is an algorithm?](https://claytonjwong.github.io/Algorithms-Stanford)
* [What is recursion?](https://en.wikipedia.org/wiki/Recursion#In_mathematics)

![](triangle.png)

[The Sierpinski triangle](https://en.wikipedia.org/wiki/Sierpinski_triangle) is a confined recursion of triangles that form a [fractal](https://en.wikipedia.org/wiki/Fractal)


## Base Case
![](base.png)

## Recursive Case
![](recurrence.png)

## Parameters
![](cn0.png)

![](rsp.png)

![](rws.png)

![](combine.png)

## Asymptotic Bound
![](asymptotic.png)

## Big-O Comparisons
![](comparison.png)
* [What is Big-O notation?](https://en.wikipedia.org/wiki/Big_O_notation)

## Pragmatic Analysis
### Example 1: Karatsuba Multiplication
* [Source Code ( trivial templates )](https://github.com/claytonjwong/Algorithms-Stanford/tree/master/course1/karatsuba_multiplication)
* [Source Code ( non-trivial strings )](https://github.com/claytonjwong/Algorithms-Stanford/tree/master/course1/karatsuba_multi_string)
#### C++
```cpp
    Type go( Type x, Type y )
    {
        if( x < 10 || y < 10 ) return x * y;
        auto i{ log(x) }, j{ log(y) }, N{ min(i,j) }, p{ pow(N/2) }, // (p)ivot
            a{ x / p }, b{ x % p },
            c{ y / p }, d{ y % p },
            u{ go(a,c) }, v{ go(a+b,c+d) }, w{ go(b,d) };
        return( u * pow( N )  +  ( v -u -w ) * pow( N/2 )  +  w );
    }
```
#### Python
```python
    def go( x, y ):
        if x < 10 or y < 10:
            return x * y
        i = log10( x )     # number of digits in x
        j = log10( y )     # number of digits in y
        N = min( i, j )    # minimum number of digits between x, y
        p = pow10( N/2 )   # pivot position 
        a = x / p          # a is the first half of x
        b = x % p          # b is the second half of x
        c = y / p          # c is the first half of y
        d = y % p          # d is the second half of y
        u = go( a, c )
        v = go( a+b, c+d )
        w = go( b, d )
        return u * pow10( N ) + ( v -u -w ) * pow10( N/2 ) + w
```

### Example 2: Merge Sort
* [Source Code](https://github.com/claytonjwong/Algorithms-Stanford/tree/master/course1/merge_sort)
#### C++
```cpp
    Collection go( Collection&& A )
    {
        if( A.size() < 2 )
            return A;
        auto pivot = A.begin() + A.size() / 2;
        return merge( go({ A.begin(), pivot }), go({ pivot, A.end() }) );
    }

    Collection merge( Collection&& lhs, Collection&& rhs, Collection res={} ) // merge (res)ult
    {
        auto L = lhs.begin(), R = rhs.begin();
        while( L != lhs.end() && R != rhs.end() )
            res.push_back( ( *L < *R )? *L++ : *R++ );
        res.insert( res.end(), L, lhs.end() ), res.insert( res.end(), R, rhs.end() ); // append left-overs ( if applicable )
        return res;
    }
```

## Citations
* **Examples & Source Code:** [Algorithms specialization from Standford University via Coursera](https://claytonjwong.github.io/Algorithms-Stanford)
  * [Karasuba Multiplication](https://github.com/claytonjwong/Algorithms-Stanford/tree/master/course1/karatsuba_multi_string)
  * [Merge Sort](https://github.com/claytonjwong/Algorithms-Stanford/tree/master/course1/merge_sort)
* **Images:** https://www.wikipedia.org
  * [What is recursion?](https://en.wikipedia.org/wiki/Recursion#In_mathematics)
  * [What is Big-O notation?](https://en.wikipedia.org/wiki/Big_O_notation)
* **Mathematical formulas:** https://www.codecogs.com/latex/eqneditor.php
