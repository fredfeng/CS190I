# Homework Assignment 1

**Due Monday, April 26, 2021 at 11:59pm (Pacific Time)**

In this homework assignment, you will use Trinity to build a toy program synthesizer for string manipulations. You will be learning the basic usage of Trinity as well as its design philosophy. Using Trinity, you will be able to create your own customized program synthesizer for various domains in a much concise and easier way.

Note: If you are passionate in programming languages techniques and are open to challenges, I have inserted some slightly more challenging problems and tips (which are marked with the cowboy face 🤠). These problems will ***NOT*** count into any of your final scores, but just for those who want to explore more of this domain. Enjoy!

## Submission

Please submit the solution files via gradescope.

In this homework, you only need to submit the following files:

- `demo_string_enumerator_problem1.py`
- `demo_string_enumerator_problem2.py`

Note: This homework should not take too long to finish. If you happened to struggle a lot, it could be my problem on stating the questions, and please don't hesitate to reach out to us about your confusions, via Slack, office hours or emails.

## Getting Started

First, get the Trinity library to your machine and switch to the `random-fix` branch (which includes functionalities that you need for this homework assignment):

```bash
git clone https://github.com/fredfeng/Trinity.git
cd Trinity/
git checkout random-fix
```

You can use Trinity from within its root folder without actually installing it. To verify the installation of Trinity, try to run the string transformation demo from the repo root:

```bash
cd Trinity/
python demo_string_enumerator.py
```

If it prints out some debugging messages followed by an info message, which says:

```
[info] Solution found: plus(plus(@param0, const(_apple_)), @param1)
```

then your environment is configured successfully.

## Problem Overview

#### The Simple String Programming Language

We now use Trinity to quickly build a synthesizer for a subset of string manipulation functions in Python, and use it to actually solve some problems. Specifically, we extract a subset of several string related methods from Python (a full documentation is available [here](https://docs.python.org/3/library/stdtypes.html#string-methods) if you are interested in their semantics) and re-pack them into our simple string domain-specific language (DSL):

```
Str  ::= concat(Str, Str) | substr(Str, Int, Int) | reverse(Str)
       | sort(Str) | tolower(Str) | toupper(Str) | join(List, Str)
List ::= split(Str, Str)
```

where `Str`, `List`, and `Int` correspond to the string, list and integer types in Python. Every function has different semantic meanings:

- `concat(Str a, Str b)`: similar to string concatenation `a+b` in Python, where in here this function simply accepts two strings and concatenate them.
- `substr(Str a, Int b, Int c)`: similar to string slicing in Python, where in here this function extracts the chars from a string from index `b` (inclusive) to `c` (exclusive).
- `reverse(Str a)`: similar to the reverse function in Python, where in here the string gets reversed.
- `sort(Str a)`: similar to the sorting function in Python, where in here this function sorts every char in string `a` in alphabetical (ASCII ascending) order.
- `tolower(Str a)`: similar to `a.lower()` in Python,  which sets all letter cases to lower.
- `toupper(Str a)`: similar to `a.upper()` in Pyhton, which sets all letter cases to upper.
- `split(Str a, Str b)`: similar to `a.split(b)` in Python, which splits the string `a` by delimiter `b`.
- `join(List a, Str b)`: similar to `b.join(a)` in Python, which concatenates a list `a` by delimiter `b`.

#### Setting up Simple String Language in Trinity

To set up your own synthesizer, you will need 3 basic components: DSL definition (spec), language interpreter and the main synthesis loop.

It's super easy to write the DSL definition, because I've done that for you already 🙂! Simply download the DSL definition files `simplestring1.tyrell` (for Problem1) and `simplestring2.tyrell` (for Problem2) from  [here](https://github.com/fredfeng/CS190I/blob/main/homework/hw1/) and place them to the `example/` folder.

> 🤠: Instead of downloading the provided file, could you come up with your own one (by observing the existing example DSLs from the `example/` folder)?

Also, you need the interpreters and main synthesis loops, which can be downloaded [here](https://github.com/fredfeng/CS190I/blob/main/homework/hw1/). To start the homework, you need to place it to the repo root folder. Note that currently both the interpreter and synthesis loop are missing some critical parts (marked with holes `??` and commented with "TBD"), and your job is to finish those missing parts.

## Problem 1 (60%)

Fill in the missing parts (**3 holes, 20% each hole**) in `demo_string_enumerator_problem1.py` so that it runs and finds the correct solution. 

Note that in this problem, you need to load `simplestring1.tyrell`. An example is given to specify the correct solution. Here you need to encode the following example into the synthesizer:

```
"ABCDE" -> "abcde"
```

which is, given the input string "ABCDE", the synthesizer is asked to produce a program written in our DSL that can produce the output "abcde" given this input. Presumably, the solution involves the `tolower` function.

Note that the Trinity repo provides you with several demos of different synthesizers, if you are running out of clues about what to fill in, read those demos (or tutorial) to learn the basic usage.

## Problem 2 (40%)

Now that you are familiar with the basic usage of Trinity, let's switch to a slightly complex example:

```
["Final", "Fantasy", "VII"] -> "Final*Fantasy*VII"
```

Note that in this problem, you need to load `simplestring2.tyrell`. This example concatenates the three strings from a list into one using delimiter "*". You are going to fill in the missing parts (**5 holes, 8% each hole**) in `demo_string_enumerator_problem2.py` so that the synthesizer runs and finds the correct solution.

> 🤠: What if you want to specify multiple examples? Try to modify the `examples` arguments and provide an extra example that says:
>
> ```["Resident", "Evil", "Village"] -> "Resident*Evil*Village"```
>
> Will the synthesizer give the same solution?
>
> 🤠: How about adding the following example?
>
> ```["Resident", "Evil", "Village"] -> "resident*evil*village"```

## 🤠: Problem 3 (0%)

As you can see the time spent for finding a correct solution can be quite long, especially when you have complicated examples, large DSLs or trivial random searching strategy. In fact, Trinity is equipped with a powerful deduction engine that helps prune the search space and find the solution even faster. However, the current setting of this homework does not enable deduction / does not benefit from deduction. Could you modify the synthesizer in Problem 2 so that it can benefit from the deduction engine?

Hint: You'll need to modify both the `simplestring2.tyrell` file and one of the demo synthesizer file.

