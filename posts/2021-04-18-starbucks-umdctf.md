# Starbucks | RE - UMDCTF 2021

### Solution

A quick look at the file tells us that this is compiled java file, so I found [decompiler online](http://www.javadecompilers.com/). After decompilation I have got this code:

```java
// 
// Decompiled by Procyon v0.5.36
// 

public class Challenge
{
    public static String f1(final String s) {
        final StringBuilder b = new StringBuilder();
        final char[] arr = s.toCharArray();
        for (int i = 0; i < arr.length; ++i) {
            b.append((char)(arr[i] + i));
        }
        return b.toString();
    }
    
    public static String f1_rev(final String s) {
        final StringBuilder b = new StringBuilder();
        final char[] arr = s.toCharArray();
        for (int i = 0; i < arr.length; ++i) {
            b.append((char)(arr[i] - i));
        }
        return b.toString();
    }
    
    public static String f2(final String s) {
        final int half = s.length() / 2;
        return String.valueOf(s.substring(half + 1)) + s.substring(0, half + 1);
    }
    
    public static String f3() {
        return f1(f2("$aQ\"cNP `_\u001d[eULB@PA'thpj]"));
    }
    
    public static void main(final String[] args) {
        System.out.println("You really thought finding the flag would be so easy?");
    }
}
```

I modified code to execute 'f3()' function and ended up with:

```java
    public static void main(final String[] args) {
        System.out.println(f3());
    }
```

Because I didn't have java compiler, again I found this [online](https://www.online-java.com/), run it and got a flag.

### Flag

UMDCTF-{**pyth0n_1s_b3tt3r**}

#### Credits

- Writeup by [HuntClauss](https://ctftime.org/user/106464)
- Solved by [HuntClauss](https://ctftime.org/user/106464)
- WaletSec 2021

#### License

**CC BY 4.0** WaletSec + HuntClauss
