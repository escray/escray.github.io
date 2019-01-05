---

layout: post
title: LeetCode 7 Reverse Integer
date: 2018-07-19

---

my solution, Runtime: 48 ms

```csharp
public class Solution {
    public int Reverse(int x) {
        var i = 0;
        long result = 0;
        var intmax = Int32.MaxValue;
        var intmin = Int32.MinValue;
 
        var flag = false;
        if (x < 0) {
            x = -x;
            flag = true;
        }
        while (x > 0)
        {
            result = result*10 + x%10;
            x /= 10;
        }

        if (result > intmax){
            return 0;
        }
        if (flag) {
            result = -result;
        }
        if (result < intmin){
            return 0;
        }
        return (int)result;
    }
}
```

Better solution, sample 44 ms submission

```csharp
public class Solution {
    public int Reverse(int x) {
        int reverse = 0;
        while(x != 0){

            if (reverse > int.MaxValue/10 || (reverse.Equals(int.MaxValue / 10 > 7))) return 0;
            if (reverse < int.MinValue/10 || (reverse.Equals(int.MinValue / 10 < -8))) return 0;
            reverse = reverse*10 + x%10;
            x = x/10;

        }
        return reverse;
    }
}
```