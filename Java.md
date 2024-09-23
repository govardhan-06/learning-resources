## Switch Case:

```
if(condtions){
  //block
  variable = x;
}


switch (variable) {
    case value1:
        // code block
        break;
    case value2:
        // code block
        break;
    // more cases...
    default:
        // default code block
}
```
## Converting types:

1. **Implicit Conversion (Widening)**
   ```java
   int num = 10;
   double d = num; // int to double
   ```

2. **Explicit Conversion (Narrowing)**
   ```java
   double d = 10.5;
   int num = (int) d; // double to int
   ```

3. **String to Integer/Double**
   ```java
   String str = "123";
   int num = Integer.parseInt(str); // String to int

   String str2 = "123.45";
   double d = Double.parseDouble(str2); // String to double
   ```

4. **Integer/Double to String**
   ```java
   int num = 123;
   String str = Integer.toString(num); // int to String

   double d = 123.45;
   String str2 = Double.toString(d); // double to String
   ```

## Rounding to decimal places

Here’s how you can round a `double` or `float` value to two decimal places using `String.format()`, `printf()`, and `Math.round()`:

1. **Using `String.format()`**
   ```java
   double value = 123.456789;
   String rounded = String.format("%.2f", value);
   System.out.println(rounded); // Output: 123.46
   ```

2. **Using `printf()`**
   ```java
   double value = 123.456789;
   System.out.printf("%.2f\n", value); // Output: 123.46
   ```

3. **Using `Math.round()`**
   ```java
   double value = 123.456789;
   double rounded = Math.round(value * 100.0) / 100.0;
   System.out.println(rounded); // Output: 123.46
   ```

## String Traversal:
```
String str = "example";
for (int i = 0; i < str.length(); i++) {
    char ch = str.charAt(i);
    System.out.println(ch);
}
```

## HashSets:

Here’s how you can use a `HashSet` in Java:

1. **Creating a `HashSet`**
   ```java
   import java.util.HashSet;

   HashSet<String> set = new HashSet<>();
   ```

2. **Adding Elements**
   ```java
   set.add("apple");
   set.add("banana");
   set.add("cherry");
   ```

3. **Removing Elements**
   ```java
   set.remove("banana");
   ```

4. **Checking if an Element Exists**
   ```java
   boolean exists = set.contains("apple");
   System.out.println(exists); // Output: true
   ```

5. **Iterating Through Elements**
   ```java
   for (String item : set) {
       System.out.println(item);
   }
   ```

6. **Size of the `HashSet`**
   ```java
   int size = set.size();
   System.out.println(size); // Output: 2
   ```

7. **Clearing All Elements**
   ```java
   set.clear();
   ```

8. **Checking if the `HashSet` is Empty**
   ```java
   boolean isEmpty = set.isEmpty();
   System.out.println(isEmpty); // Output: true
   ```
## bitwise operators 

Bitwise operators in Java are used to perform operations on the binary representations of integers. Here's a quick overview:

1. **AND (`&`)**: Performs a bitwise AND operation. Each bit of the result is 1 if the corresponding bits of both operands are 1; otherwise, it is 0.
   ```java
   int a = 5; // 0101 in binary
   int b = 3; // 0011 in binary
   int result = a & b; // 0001 in binary (1 in decimal)
   ```

2. **OR (`|`)**: Performs a bitwise OR operation. Each bit of the result is 1 if at least one of the corresponding bits of the operands is 1.
   ```java
   int result = a | b; // 0111 in binary (7 in decimal)
   ```

3. **XOR (`^`)**: Performs a bitwise XOR operation. Each bit of the result is 1 if the corresponding bits of the operands are different; otherwise, it is 0.
   ```java
   int result = a ^ b; // 0110 in binary (6 in decimal)
   ```

4. **Complement (`~`)**: Inverts all the bits of the operand.
   ```java
   int result = ~a; // 1010 in binary (in decimal, this is -6 due to sign bit)
   ```

5. **Left Shift (`<<`)**: Shifts the bits of the number to the left by a specified number of positions. This operation fills the vacated bits on the right with 0s.
   ```java
   int result = a << 1; // 1010 in binary (10 in decimal)
   ```

6. **Right Shift (`>>`)**: Shifts the bits of the number to the right by a specified number of positions. The sign bit is used to fill the vacated bits on the left.
   ```java
   int result = a >> 1; // 0010 in binary (2 in decimal)
   ```

7. **Unsigned Right Shift (`>>>`)**: Shifts the bits of the number to the right by a specified number of positions, filling the vacated bits on the left with 0s, regardless of the sign bit.
   ```java
   int result = a >>> 1; // 0010 in binary (2 in decimal)
   ```

These operators can be useful for low-level programming, such as in systems programming, graphics, or performance optimization tasks.

## String Function:
To capitalize an entire word (all characters in uppercase) in Java, use:

```java
String capitalizedWord = yourString.toUpperCase();
```

This will convert the entire string to uppercase. For example:

```java
String word = "hello";
String capitalizedWord = word.toUpperCase(); // Output: "HELLO"
```

```
str.toLowerCase();
```
for lower casing 


### to get the end of an array with bigger size but lower number of elements:

```java
for(int i=0; c[i]!='\0'; i++)
```

## TO TAKE CHAR AS INPUT 

To take a character as input in Java, you can use the `Scanner` class and its `next().charAt(0)` method. This method reads a `String` from the user and extracts the first character of that `String`.

Here's an example:

```java
import java.util.Scanner;

public class CharacterInput {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a character: ");
        char input = scanner.next().charAt(0);

        System.out.println("You entered: " + input);

        scanner.close();
    }
}
```

### Explanation:
- `Scanner scanner = new Scanner(System.in);` creates a `Scanner` object to read input from the console.
- `scanner.next().charAt(0);` reads the input as a `String` and then `charAt(0)` extracts the first character of that `String`.
- The character is then stored in the variable `input` and can be used as needed.

This method ensures you capture a single character from the user's input.


## To find number of digits in a number

```
int numDigits = String.valueOf(number).length();
```

## String comparison

In Java, string comparison can be done using several methods depending on the level of comparison you need (case-sensitive, case-insensitive, etc.). Here are the common ways to compare strings in Java:

### 1. Using `equals()` Method
The `equals()` method compares the content of two strings for equality in a case-sensitive manner.

```java
public class StringComparison {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "Hello";
        String str3 = "hello";

        // Case-sensitive comparison
        boolean result1 = str1.equals(str2); // true
        boolean result2 = str1.equals(str3); // false

        System.out.println("str1 equals str2: " + result1);
        System.out.println("str1 equals str3: " + result2);
    }
}
```

### 2. Using `equalsIgnoreCase()` Method
The `equalsIgnoreCase()` method compares two strings, ignoring case considerations.

```java
public class StringComparison {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "hello";

        // Case-insensitive comparison
        boolean result = str1.equalsIgnoreCase(str2); // true

        System.out.println("str1 equalsIgnoreCase str2: " + result);
    }
}
```

### 3. Using `compareTo()` Method
The `compareTo()` method compares two strings lexicographically. It returns:
- `0` if the strings are equal,
- A positive number if the first string is lexicographically greater than the second string,
- A negative number if the first string is lexicographically less than the second string.

```java
public class StringComparison {
    public static void main(String[] args) {
        String str1 = "Apple";
        String str2 = "Banana";
        String str3 = "Apple";

        // Lexicographical comparison
        int result1 = str1.compareTo(str2); // Negative value
        int result2 = str1.compareTo(str3); // 0

        System.out.println("str1 compareTo str2: " + result1);
        System.out.println("str1 compareTo str3: " + result2);
    }
}
```

### 4. Using `compareToIgnoreCase()` Method
The `compareToIgnoreCase()` method works like `compareTo()`, but it ignores case differences.

```java
public class StringComparison {
    public static void main(String[] args) {
        String str1 = "Apple";
        String str2 = "apple";

        // Lexicographical comparison ignoring case
        int result = str1.compareToIgnoreCase(str2); // 0

        System.out.println("str1 compareToIgnoreCase str2: " + result);
    }
}
```

### 5. Using `==` Operator
The `==` operator compares the references (addresses in memory) of two strings, not their content. Use it with caution as it checks if both strings point to the same object.

```java
public class StringComparison {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "Hello";
        String str3 = new String("Hello");

        // Reference comparison
        boolean result1 = (str1 == str2); // true, because of string interning
        boolean result2 = (str1 == str3); // false, because str3 is a new object

        System.out.println("str1 == str2: " + result1);
        System.out.println("str1 == str3: " + result2);
    }
}
```

##String reversal

In Java, you can reverse a string in several ways. Below are some common methods:

### 1. Using `StringBuilder` or `StringBuffer`
Java's `StringBuilder` and `StringBuffer` classes have a `reverse()` method that you can use directly.

```java
public class StringReversal {
    public static void main(String[] args) {
        String original = "Hello, World!";
        
        // Using StringBuilder
        StringBuilder sb = new StringBuilder(original);
        String reversed = sb.reverse().toString();
        
        System.out.println("Reversed String: " + reversed);
    }
}
```

### 2. Using a Loop
You can reverse a string by iterating from the end to the beginning and building a new string.

```java
public class StringReversal {
    public static void main(String[] args) {
        String original = "Hello, World!";
        String reversed = "";

        for (int i = original.length() - 1; i >= 0; i--) {
            reversed += original.charAt(i);
        }

        System.out.println("Reversed String: " + reversed);
    }
}
```

### 3. Using Recursion
You can reverse a string recursively by breaking the problem down into smaller subproblems.

```java
public class StringReversal {
    public static void main(String[] args) {
        String original = "Hello, World!";
        String reversed = reverseRecursively(original);
        
        System.out.println("Reversed String: " + reversed);
    }

    public static String reverseRecursively(String str) {
        if (str.isEmpty()) {
            return str;
        }
        return reverseRecursively(str.substring(1)) + str.charAt(0);
    }
}
```

### 4. Using Java 8 Streams
If you prefer using functional programming, Java 8 streams provide a concise way to reverse a string.

```java
import java.util.stream.Collectors;

public class StringReversal {
    public static void main(String[] args) {
        String original = "Hello, World!";
        
        String reversed = original.chars()
                                  .mapToObj(c -> (char) c)
                                  .collect(Collectors.collectingAndThen(
                                      Collectors.toList(),
                                      lst -> { 
                                          java.util.Collections.reverse(lst); 
                                          return lst.stream();
                                      }))
                                  .map(String::valueOf)
                                  .collect(Collectors.joining());
                                  
        System.out.println("Reversed String: " + reversed);
    }
}
```

### Printing %

Each of these methods achieves the same result—reversing the given string—but may be suitable for different use cases depending on your needs or constraints.

In Java, when you use the `printf` or `String.format` methods and want to include a percent symbol (`%`) in the output, you need to escape it by doubling it (`%%`). This is because the percent symbol is used as a special character for formatting instructions (e.g., `%d` for integers, `%f` for floating-point numbers).

Here's how you can include a percent symbol in your formatted output:

### Example Using `System.out.printf`
```java
public class PercentSymbolExample {
    public static void main(String[] args) {
        double value = 85.5;
        
        // Using printf to include a percent symbol
        System.out.printf("The success rate is %.1f%%.%n", value);
    }
}
```

### Example Using `String.format`
```java
public class PercentSymbolExample {
    public static void main(String[] args) {
        double value = 85.5;
        
        // Using String.format to include a percent symbol
        String result = String.format("The success rate is %.1f%%.", value);
        System.out.println(result);
    }
}
```

### Output
```
The success rate is 85.5%.
```

### Explanation
- **`%%`**: When using `printf` or `String.format`, `%%` is used to print a single `%` symbol in the output.
- **Formatting Specifiers**: Other specifiers like `%.1f` format the number to one decimal place.

Using `%%` in formatted strings is a simple and effective way to include the percent symbol in your Java output.

For content comparison, it's always best to use `equals()` or `compareTo()` methods. The `==` operator should only be used if you specifically need to compare the references of the strings.
