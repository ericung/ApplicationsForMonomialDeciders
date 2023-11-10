# Applications of Monomial Deciders

This is part 2 of the article, "[A Language of Polynomials](https://github.com/ericung/languageofpolynomials)", with concrete examples of how to use it including constructing the one way function using the picking function.

## 1. Starting With A Theorem Of Infiniteness

![Starting With A Theorem Of Infiniteness](https://i.seadn.io/s/raw/files/355f7480e3c00dca91baa5e6396a3c1e.jpg?auto=format&dpr=1&w=1000)

## 2. Mapping Out Worlds

![Mapping Out Worlds](https://i.seadn.io/s/raw/files/d7aa0fb86ec30bdf2e6cd21f9ff99684.jpg?auto=format&dpr=1&w=1000)

## 3. Euler's Constant

![Euler's Constant](https://i.seadn.io/s/raw/files/89d733a5810431c70a9ca749ac1ad5ef.jpg?auto=format&dpr=1&w=1000)

## 4. Sketching Into Code

![Sketching Into Code](https://i.seadn.io/s/raw/files/a41d6f9e8ada79ef18b0ead8acc9a4e7.jpg?auto=format&dpr=1&w=1000)

```cs
bool generalizedMD(int y)
{
    if (y == 0)
    {
        return true;
    }
    var s = y;
    while (s >= 0)
    {
        for (int i = 0; i < 2; i++)
        {
            for (int j = 0; j < 4; j++)
            {
                if (s == 0 && (j == 0 || j == 2) && i == 0)
                {
                    return true;
                }
                else if (s < 0)
                {
                    return false;
                }
                s -= 1;
            }
        }
    }
    return true;
}
```

## 5. Gather Some Data
![Gathering Some Data](https://i.seadn.io/s/raw/files/eb31664e64ddaf6b9f375981c29343c6.jpg?auto=format&dpr=1&w=1000)

```cs
// Generates negatives from a general monomial decider represented as an algorithm so
// that we can collect data about the negatives
int[] Generator(int max)
{
    int[] result = new int[max + 1];
    int x = 0;
    int negatives = 0;
    int i = 0;
    while (x < max + 1)
    {
        int num = 2 * (Convert.ToInt32(Math.Pow(x, 2)));
        if (generalizedMD(i))
        {
            // A simple verifier
            if (num == i)
            {
                Console.WriteLine(negatives);
                Console.WriteLine("f(" + x + ") = " + i);
                result[x] = i;

                x++;
                negatives = 0;
            }
            else
            {
                negatives++;
            }
        }
        i++;
    }

    return result;
}
```

[Logs for the curious.](Source/ApplicationsForMonomialDeciders/Logs/MDxx/generalizedMD.txt)

## 6. Representing Monomial Deciders As Code
![Representing Monomial Deciders As Code](https://i.seadn.io/s/raw/files/a958de4ea888bf0334fb40748f204510.jpg?auto=format&dpr=1&w=1000)

```cs
// After getting some log results, we can construct a decider
bool MonomialDecider2xx(int y)
{
    var total = 0;
    var hits = 0;
    var diff = 1;
    var isEven = 0;
    var s = 0;

    while (s <= y)
    {
        for (int i = 0; i < 2; i++)
        {
            for (int j = 0; j < 2; j++)
            {
                for (int k = 0; k < 2; k++)
                {
                    if ((i == 0)&&(j == 0 || j == 1)&&(k == 0))
                    {
                        if (hits == total)
                        {
                            if (s == y)
                            {
                                Console.WriteLine(s + ": Hits: " + total);
                                return true;
                            }
                            else if (s > y)
                            {
                                return false;
                            }

                            total += diff;
                            isEven++;
                            if (isEven % 3 == 2)
                            {
                                isEven = 0;
                                diff += 2;
                            }
                        }

                        hits++;
                    }
                    s++;
                }
            }
        }
    }

    return false;
}
```

[Logs for the curious.](Source/ApplicationsForMonomialDeciders/Logs/MDxx/md2xx.txt)

## 7. Negative Numbers

![Negative Numbers](https://i.seadn.io/s/raw/files/568874f7852af4b7ee4cc2d3fd58f309.jpg?auto=format&dpr=1&w=1000)

## 8. Pi

![Pi](https://i.seadn.io/s/raw/files/ed6b0ade60a1c9a561ff82b6923f5f2d.jpg?auto=format&dpr=1&w=1000)

## 9. Fibonacci

![Fibonnaci](https://i.seadn.io/s/raw/files/6800e6a3ac49fd70869c386db6c1cf66.jpg?auto=format&dpr=1&w=1000)

Let's take apart the fibonacci sequence and try to find some patterns.

```cs
int fibonacci(int n)
{
    if (n == 0)
    {
        return 0;
    }

    int y = 1;
    int y1 = 1;
    int y2 = 0;

    for(int i = 1; i < n; i++)
    {
        y = y1 + y2;
        y2 = y1;
        y1 = y;
    }

    return y;
}
```

Here's the log for the first 14 entries.

```
f(	0	) =		0		Ex = 0		eY = 0
f(	1	) =		1		Ex = 1		eY = 1
f(	2	) =		1		Ex = 0		eY = 1
f(	3	) =		2		Ex = 1		eY = 0
f(	4	) =		3		Ex = 0		eY = 1
f(	5	) =		5		Ex = 1		eY = 1
f(	6	) =		8		Ex = 0		eY = 0
f(	7	) =		13		Ex = 1		eY = 1
f(	8	) =		21		Ex = 0		eY = 1
f(	9	) =		34		Ex = 1		eY = 0
f(	10	) =		55		Ex = 0		eY = 1
f(	11	) =		89		Ex = 1		eY = 1
f(	12	) =		144		Ex = 0		eY = 0
f(	13	) =		233		Ex = 1		eY = 1
f(	14	) =		377		Ex = 0		eY = 1
```

[Logs for the curious.](Source/ApplicationsForMonomialDeciders/Logs/Fibonacci/fibonacci.txt)

## 10. Analysis Of Parity In Fibonacci

![10AnalysisOfParityInFibonacci](https://i.seadn.io/s/raw/files/c34040025bc28cb993857bff5edfbbe9.jpg?auto=format&dpr=1&w=1000)

## 11. Redrawing the Fibonacci Sequence

![11RedrawingTheFibonacciSequence](https://i.seadn.io/s/raw/files/bf5eb9dce0f79879f1d58ad07d41218f.jpg?auto=format&dpr=1&w=1000)

Fibonacci generator with the set of generator functions.

```cs
int fibonacciGenerator(int n)
{
    int stateX = 0;
    int stateY = 1;
    int stateZ = 1;
    int cycles = 0;

    while (cycles <= n)
    {
        cycles++;

        if (cycles > n)
        {
            return stateX;
        }

        stateX = stateY + stateZ;
        Console.WriteLine("stateX: " + stateX + "\tstateY: " + stateY + "\tstateZ: " + stateY);
        
        cycles++;

        if (cycles > n)
        {
            return stateY;
        }

        stateY = stateX + stateZ;
        Console.WriteLine("stateX: " + stateX + "\tstateY: " + stateY + "\tstateZ: " + stateY);

        cycles++;

        if (cycles > n)
        {
            return stateZ;
        }

        stateZ = stateX + stateY;
        Console.WriteLine("stateX: " + stateX + "\tstateY: " + stateY + "\tstateZ: " + stateY);
    }

    return stateX;
}
```

[Logs for the curious.](Source/ApplicationsForMonomialDeciders/Logs/Fibonacci/fibonacciGenerator.txt)

## 12. The Fibonacci Decider

![12FibonacciDecider](https://i.seadn.io/s/raw/files/f3bc75ac1efffa0f55c1a9b6310378dc.jpg?auto=format&dpr=1&w=1000)

Given a sequence of length six, we can decide if it forms a valid fibonacci sequence.\
The following is a log of calculations.

```

x1 = 144, y1 = 89, z1 = 55, x2 = 34, y2 = 21, z2 = 13

144 = 89 - 13 + 34 - 21 + 55 = 144
89 = 13 - 34 + 21 - 55 + 144 = 89
13 = 34 - 21 + 55 - 144 + 89 = 13
34 = 21 - 55 + 144 - 89 + 13 = 34
21 = 55 - 144 + 89 - 13 + 34 = 21
55 = 144 - 89 + 13 - 34 + 21 = 55

```

# 13. The Fibonacci Picking Function

![13FibonacciPickingFunction](https://i.seadn.io/s/raw/files/fc6c93a7b2a2b58d89b98deb05cdf3ff.jpg?auto=format&dpr=1&w=1000)

-----

## References

Ung, E. (2023). [A Language of Polynomials](https://github.com/ericung/languageofpolynomials) (Version 1.0.0). https://github.com/ericung/languageofpolynomials

Hamming, R. W. (1986). *Numerical methods for scientists and engineers.* Courier Corporation.

Ung, E. (2023). [Inferring Lindenmayer Systems](https://github.com/ericung/InferrenceSystems/blob/master/Resources/lindenmayer_systems.pdf). 1(1), 1–6. https://github.com/ericung/InferrenceSystems/blob/master/Resources/lindenmayer_systems.pdf
