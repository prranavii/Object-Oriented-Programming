# Exception Handling in Java

Exception handling in Java is a mechanism used to handle runtime errors so that a program can continue or terminate gracefully instead of crashing unexpectedly.

## Main Keywords

- **`try`** — contains code that may cause an exception.
- **`catch`** — handles the exception.
- **`finally`** — executes whether an exception occurs or not, commonly for cleanup.
- **`throw`** — explicitly throws an exception.
- **`throws`** — declares that a method may throw an exception.

## Example

```java
public class ExceptionExample {
    public static void main(String[] args) {
        try {
            int a = 10;
            int b = 0;
            int result = a / b;
            System.out.println(result);
        } catch (ArithmeticException e) {
            System.out.println("Cannot divide by zero.");
        } finally {
            System.out.println("Program finished.");
        }
    }
}
