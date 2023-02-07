# Nested Conditionals

## Learning Goals

- Continue learning about conditionals.
- Take a look at `if` statements inside of `if` statements.

## Introduction

In the previous lesson, we introduced a chained conditional statements using the
`else if` statement. Stated before, we said that an `if` block could hold more
than one statement. But what if we want one of those statements to be another
`if` statement? Is that possible?

The answer is yes! Since `if` statements can contain multiple statements inside
their `if` block, they can also contain other `if` statements. This is called
**nested conditionals**.

## Nested Conditional Example

Consider the following changes to the program we have been working with:

```java
import java.util.InputMismatchException;
import java.util.Scanner;

public class GradeExample {
    public static void main (String[] args) {
        Scanner scanner = new Scanner(System.in);

        try {
            // Prompt the user to enter a numeric grade from 0 to 100
            System.out.println("Enter a numeric grade from 0 - 100:");
            int grade = scanner.nextInt();

            // A passing grade is a 70 or higher
            if (grade >= 70) {
                System.out.println("Congrats! You passed!");
                if (grade >= 90) {
                    System.out.println("Wow! You got an A!");
                    System.out.println("Great job!");
                } else {
                    System.out.println("Great job!");
                }
            }

        } catch (InputMismatchException exception) {
            System.out.println("Invalid input");
        }
    }
}
```

In the example above, we want to further customize the greeting message for
students that pass their test. We want to give an extra congratulations to
those students who receive a score of 90 and up; so we check to see if their
grade is greater than or equal to a 90 and display a message if that is the
case. If not, we simply tell congratulate them on passing their test and let
them know they did a great job.

Let's take a look at what happens when the user enters 85 for a grade in the
debugger:

![if-statement-breakpoint](https://curriculum-content.s3.amazonaws.com/java-mod-1/if-statement/intellij-debugger-if-statement-breakpoint-3.PNG)

We will first compare the value in the variable `grade` with the passing grade
of 70 in the first `if` statement. Since `grade` is storing the value of 85, we
will evaluate `85 >= 70` to be `true`. As we have seen previously, the code will
then enter the `if` block.

Let's step-over two more times until we reach the line `if (grade >= 90)`:

![inner-if-statement](https://curriculum-content.s3.amazonaws.com/java-mod-1/if-statement/intellij-debugger-if-statement-breakpoint-4.PNG)

At this point, we encounter another `if` statement! Just like the previous outer
`if` statement, Java will evaluate the conditional clause. This conditional
clause is `grade >= 90`. In this case, `85 >= 90` will evaluate to `false`,
causing the execution to skip on down to the `else` statement within this inner
`if-else` block:

![else-block-execution](https://curriculum-content.s3.amazonaws.com/java-mod-1/if-statement/intellij-debugger-else-block-execution-2.PNG)

If we resume the program, we'll see that when the user enters 85, the output in
the console looks like this:

```text
Enter a numeric grade from 0 - 100:
85
Congrats! You passed!
Great job!
```

Now let's take a look at what happens when the user enters 90 instead for a
grade in the debugger:

![if-statement-breakpoint](https://curriculum-content.s3.amazonaws.com/java-mod-1/if-statement/intellij-debugger-if-statement-breakpoint-5.PNG)

Just as before, we will evaluate the conditional clause of the outer `if`
statement to be `90 >= 70`. This will return `true` so we expect to fall into
the outer `if` block. Let's step-over two more times until we reach the line
`if (grade >= 90)` again:

![inner-if-statement](https://curriculum-content.s3.amazonaws.com/java-mod-1/if-statement/intellij-debugger-if-statement-breakpoint-6.PNG)

Like before, the code will evaluate the conditional clause of this inner `if`
statement. But unlike the previous input, when we evaluate `grade >= 90`, which
is equivalent to `90 >= 90` in this case, it will result in a `true`. So instead
of skipping down to the `else` block like we did above, this time, we will enter
into the inner `if` block:

![if-block-execution](https://curriculum-content.s3.amazonaws.com/java-mod-1/if-statement/intellij-debugger-if-block-execution-2.PNG)

If we resume the program, we'll see that when the user enters 90, the output in
the console looks like this:

```text
Enter a numeric grade from 0 - 100:
90
Congrats! You passed!
Wow! You got an A!
Great job!
```

Now, we may have noticed that no matter if the value of `grade` is considered an
`A` or not, as long as it is passing, we tell the user "Great job!" Can we modify
the code in the previous example to remove the duplicated line of code between
the case where the student's grade is greater than or equal to 90 and the case
where the student's grade is less than 90 but greater than or equal to 70?

The answer is yes! Consider the following code below that removes the duplicated
line:

```java
import java.util.InputMismatchException;
import java.util.Scanner;

public class GradeExample {
    public static void main (String[] args) {
        Scanner scanner = new Scanner(System.in);

        try {
            // Prompt the user to enter a numeric grade from 0 to 100
            System.out.println("Enter a numeric grade from 0 - 100:");
            int grade = scanner.nextInt();

            // A passing grade is a 70 or higher
            if (grade >= 70) {
                System.out.println("Congrats! You passed!");
                if (grade >= 90) {
                    System.out.println("Wow! You got an A!");
                }
                System.out.println("Great job!");
            }

        } catch (InputMismatchException exception) {
            System.out.println("Invalid input");
        }
    }
}
```

In this case, the `else` block was unnecessary since "Great job!" would be
printed to the console regardless as long as the grade is considered a passing
grade.

Let's do knowledge check based off of the code above!

<details>
  <summary>What do we expect to be printed <i>after</i> the user enters in 60 for the grade?</summary>

  <p>Answer:<br></p>

  <p>Nothing. There will be no lines printed after the user enters in 60 for a grade since there is no else statement after the <code>if (grade >= 70)</code></p>

</details>

<details>
  <summary>What do we expect to be printed <i>after</i> the user enters in 70 for the grade?</summary>

  <p>Answer:<br></p>

  <p><code>Congrats! You passed!</code><br><code>Great job!</code></p>

</details>

<details>
  <summary>What do we expect to be printed <i>after</i> the user enters in 92 for the grade?</summary>

  <p>Answer:<br></p>

  <p><code>Congrats! You passed!</code><br><code>Wow! You got an A!</code><br><code>Great job!</code></p>

</details>
