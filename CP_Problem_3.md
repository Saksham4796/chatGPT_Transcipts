> Write the JAVA program for the below problem statement: An additive number is a string whose digits can form an additive sequence. A valid additive sequence should contain at least three numbers. Except for the first two numbers, each subsequent number in the sequence must be the sum of the preceding two. Given a string containing only digits, return true if it is an additive number or false otherwise. Note: Numbers in the additive sequence cannot have leading zeros, so sequence 1, 2, 03 or 1, 02, 3 is invalid. Example 1: Input: "112358" Output: true Explanation: The digits can form an additive sequence: 1, 1, 2, 3, 5, 8. 1 + 1 = 2, 1 + 2 = 3, 2 + 3 = 5, 3 + 5 = 8 Example 2: Input: "199100199" Output: true Explanation: The additive sequence is: 1, 99, 100, 199. 1 + 99 = 100, 99 + 100 = 199 Constraints: 1 <= num.length <= 35 num consists only of digits.

Here's the Java program for the given problem statement:

java

```java
public class AdditiveNumber {

    public static boolean isAdditiveNumber(String num) {
        int n = num.length();
        for (int i = 1; i <= n / 2; i++) {
            for (int j = 1; Math.max(j, i) <= n - i - j; j++) {
                if (isValid(i, j, num)) {
                    return true;
                }
            }
        }
        return false;
    }

    public static boolean isValid(int i, int j, String num) {
        if (num.charAt(0) == '0' && i > 1) {
            return false;
        }
        if (num.charAt(i) == '0' && j > 1) {
            return false;
        }
        String sum;
        Long x1 = Long.parseLong(num.substring(0, i));
        Long x2 = Long.parseLong(num.substring(i, i + j));
        for (int start = i + j; start != num.length(); start += sum.length()) {
            x2 = x1 + x2;
            x1 = x2 - x1;
            sum = x2.toString();
            if (!num.startsWith(sum, start)) {
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        System.out.println(isAdditiveNumber("112358")); //true
        System.out.println(isAdditiveNumber("199100199")); //true
        System.out.println(isAdditiveNumber("1023")); //false
    }
}
```

Explanation: The `isAdditiveNumber` method checks whether a given string is an additive number or not. It takes a string `num` as input and returns a boolean value indicating whether the string is an additive number or not.

The method starts by iterating through all possible combinations of the first two numbers in the additive sequence. For each combination, it checks whether the remaining digits form a valid additive sequence using the `isValid` method.

The `isValid` method takes three arguments: `i`, `j`, and `num`. `i` and `j` represent the lengths of the first two numbers in the additive sequence, and `num` is the input string.

The method checks whether the first two numbers have leading zeros, and if so, returns false. Then it iterates through the remaining digits and checks whether each subsequent number is the sum of the preceding two. If any of the numbers are not the sum of the preceding two, the method returns false. If all the numbers are valid, the method returns true.

Finally, the main method calls the `isAdditiveNumber` method with three different inputs and prints the corresponding boolean values.