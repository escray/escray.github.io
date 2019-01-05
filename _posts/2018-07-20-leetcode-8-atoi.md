---

layout: post
title: LeetCode 8 atoi
date: 2018-07-20

---

first version, Runtime: 120 ms

```csharp

public class Solution {
    public int MyAtoi(string str) {
        var i = 0;
        var intmax = int.MaxValue;
        var intmin = int.MinValue;
        var flag = false;
        var f = true;
        var blank = true;
        long result = 0;
        
        for (i=0; i<str.Length; i++) {
            if (blank && str[i] == ' ') continue;
            blank = false;
            
            if (f && i < str.Length && str[i] == '+') { 
                i++;
            }
            else if (f && i < str.Length && str[i] == '-' ) {
                flag = true;
                i++;
            }
            f = false;
            
            if (i < str.Length && str[i] >= '0' && str[i] <= '9') {
                // (int)Char.GetNumericValue('8')
                // result = result*10 + Int32.Parse(str[i].ToString());
                result = result*10 + (int)Char.GetNumericValue(str[i]);
                if (flag && -result <= intmin) {
                    return intmin;
                }
                else if (result > intmax) {
                    return intmax;
                }
            }
            else{
                break;
            }            
        }
        
        if (flag) {
            result = -result;
        }
        if (result < intmin) {
            return intmin;
        }
        if (result > intmax) {
            return intmax;
        }
        
        
        return (int)result;
    }
}

```

second version, 96 ms

```csharp
public class Solution {
    public int MyAtoi(string str) {
        var i = 0;
        var intmax = int.MaxValue;
        var intmin = int.MinValue;
        var flag = false;
        long result = 0;
        
        str = str.TrimStart();
        
        if (str.Length == 0) {
            return 0;
        }
        
        if (str[0] == '-') {
            flag = true;
            i++;
        }
        else if (str[0] == '+') {
            i++;
        }
        
        for (; i<str.Length; i++) {
            if (str[i] >= '0' && str[i] <= '9') {
                result = result*10 + (int)Char.GetNumericValue(str[i]);
            }
            else{
                break;
            }  
            
            if (result > intmax) {
                return flag ? intmin : intmax;
            }
        }
        
        if (flag) {
            result = -result;
        }
        
        return (int)result;
    }
}
```

better version, 88 ms
```csharp
public class Solution {
    public int MyAtoi(string str) {
        if (string.IsNullOrEmpty(str))
            return 0;
        
        String s = str.Trim();        
        if (string.IsNullOrEmpty(s))
            return 0;       
                
        List<char> lstValidChars = new List<char>() { '-', '+'};
        List<char> lstValidDigits = new List<char>() { '0', '1', '2', '3', '4', '5', '6', '7', '8', '9' };       
               
        
        int i = 0;
        while(i < s.Length)
        {
            if (i == 0)
            {
                if (!(lstValidChars.Contains(s[i]) || lstValidDigits.Contains(s[i])))
                    break;               
            }
            else
            {
                if (!lstValidDigits.Contains(s[i]))
                    break;
            }
            i++;
        }
        
        s = s.Substring(0, i);
        int value = 0;
        try
        {
            value = int.Parse(s);
        }
        catch(OverflowException ex)
        {
            if (s[0] == '-')
                value = int.MinValue;
            else
                value = int.MaxValue;
        }
        catch(Exception e)
        {
            value = 0;
        }
        
        
        return value;
    }
}
```

best version, 84 ms
```csharp
public class Solution {
    public int MyAtoi(string str) {
        if(str == null || str.Length == 0) return 0;
        int flag = 0;
        int index = 0;
        char[] arr = str.ToCharArray();
        int res = 0;
        bool overflow = false;
        while(index < str.Length && (arr[index] == ' ' || arr[index] == '\t' || arr[index] == '\n')){
            index++;
        }
        if(index < str.Length){
            switch(arr[index]){
                case '+' :
                    flag = 1;
                    index++;
                    break;
                case '-' :
                    flag = -1;
                    index++;
                    break;
                default :
                    flag = 1;
                    break;
            }
        }
        
        while(index < str.Length && arr[index] != '\0'){
            if(!Char.IsDigit(arr[index])) break;
            else
                if(res > int.MaxValue/10){
                    overflow = true;
                    break;
                }
                res = res*10 + (int)(arr[index] - '0');
                if(res < 0){
                    overflow = true;
                    break;
                }
                index++;
            
        }
        if(overflow)
            return flag > 0 ? int.MaxValue : int.MinValue;
        return flag * res;
    }
}
```