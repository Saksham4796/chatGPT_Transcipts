> Write JAVA code for the below problem statement: Given an integer n, count the total number of digit 1 appearing in all non-negative integers less than or equal to n. Example 1: Input: n = 13 Output: 6 Example 2: Input: n = 0 Output: 0 Constraints: 0 <= n <= 10^9 Use the below template: class Solution { public int countDigitOne(int n) { } } Solve using recursion.

Here's the Java code that solves the given problem statement using recursion:

python

```python
class Solution {
    public int countDigitOne(int n) {
        if (n <= 0) {
            return 0;
        }
        if (n < 10) {
            return 1;
        }
        String str = Integer.toString(n);
        int len = str.length();
        int firstDigit = str.charAt(0) - '0';
        int remainingNumber = Integer.parseInt(str.substring(1));
        int numOnesFirstDigit = 0;
        if (firstDigit > 1) {
            numOnesFirstDigit += Math.pow(10, len - 1);
        } else {
            numOnesFirstDigit += Integer.parseInt(str.substring(1)) + 1;
        }
        int numOnesRemainingDigits = (len - 1) * firstDigit * (int) Math.pow(10, len - 2);
        return numOnesFirstDigit + numOnesRemainingDigits + countDigitOne(remainingNumber);
    }
}
```

Here's how the code works:

1.  The `countDigitOne` function takes an integer `n` as input and returns the total number of digit 1 appearing in all non-negative integers less than or equal to `n`.
    
2.  The base case is when `n` is less than or equal to 0, in which case we return 0. If `n` is a single-digit number, we return 1 if `n` is greater than 0 and 0 otherwise.
    
3.  We convert the input `n` into a string `str` so that we can easily access its individual digits. We also compute the length of the string `len`, the value of its first digit `firstDigit`, and the remaining digits `remainingNumber`.
    
4.  We then compute the number of ones that appear in the first digit of `n` using the following logic:
    
    a. If the first digit is greater than 1, then there are `10^(len-1)` numbers that start with that digit, and each of these numbers has a 1 in the first digit.
    
    b. If the first digit is 1, then we need to count the number of ones in the remaining digits as well. We can do this by taking the `remainingNumber` and adding 1 to it, since there is one number (`n` itself) that has a 1 in the first digit.
    
    c. If the first digit is 0, then there are no numbers that start with a 1, so we don't need to count anything.
    
5.  We then compute the number of ones that appear in the remaining digits of `n` using the following logic:
    
    a. There are `len-1` remaining digits after the first digit.
    
    b. Each of these digits can be any digit from 0 to 9, so there are `10^(len-2)` possible combinations.
    
    c. For each combination, there is exactly one digit that is a 1, so there are `len-1` ones that appear in the remaining digits of `n`.
    
    d. Multiplying the number of ones in the first digit by the number of possible combinations for the remaining digits gives us the total number of ones that appear in the remaining digits.
    
6.  We add up the number of ones that appear in the first digit and the number of ones that appear in the remaining digits, and recursively call the `countDigitOne` function on the `remainingNumber`.
    
7.  We return the sum of the three values computed in steps 4, 5, and 6.