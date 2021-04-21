# Homework Assignment 2

**Due Monday, May 3, 2021 at 11:59pm (Pacific Time)**

In this homework, you will be using Venti ([https://github.com/chyanju/Venti.git](https://github.com/chyanju/Venti.git)) to build clients to verify smart contracts.

Note: If you are passionate in programming languages techniques and are open to challenges, I have inserted some slightly more challenging problems and tips (which are marked with the cowboy face 🤠). These problems will ***NOT*** count into any of your final scores, but just for those who want to explore more of this domain. Enjoy!

## Submission

Please submit the solution files via gradescope.

In this homework, you only need to submit the following files:

- `task1-1.txt` required by Problem 1, Task 1-1
- `task1-2.txt` required by Problem 1, Task 1-2
- `task2-1.txt` required by Problem 2, Task 2-1
- `P2-config.json` required by Problem 2, Task 2-2
- `task2-3.json` or `task2-3.txt` required by Problem 2, Task 2-3

Note: This homework does require sometime to understand the background knowledge, but should be relatively straightforward to finish the tasks if you are clear about the mechanism of the environment and the tasks. If you happened to struggle a lot more than expected, it could be my problem on stating the questions, and please don't hesitate to reach out to us about your confusions, via Slack, office hours or emails.

## Getting Started

First set up the Venti and Solidity environment by the following steps.

#### Setting up Solidity Environment

Follow the setup instructions of `solc-select` to install the Solidity environment here: [https://github.com/crytic/solc-select](https://github.com/crytic/solc-select). After the configuration is done, switch to solc version `0.7.3` by:

```bash
solc-select use 0.7.3
```

Note that before you switch your `solc` version, you'll need to install Solidity version `0.7.3` if you haven't done so after the configuration. After than, issue:

```bash
solc --version
```

and if you see the following information (or something similar), then you are good to go:

```
solc, the solidity compiler commandline interface
Version: 0.7.3+commit.9bfce1f6.Darwin.appleclang
```

#### Setting up Venti Environment

**<u>*(Please follow the instructions below instead of the guide from the Venti repo; that guide is meant for development)*</u>**

Venti requires Racket 7.x, Rosette 3.x and Python 3.x.

It should be relatively easy for you to get a Python 3.x. If you still feel confused, consider setting up an Anaconda environment. See: [https://www.anaconda.com/products/individual](https://www.anaconda.com/products/individual). 

In this homework, Racket 7.7 is recommended. Go to [https://download.racket-lang.org/racket-v7.7.html](https://download.racket-lang.org/racket-v7.7.html) and follow the official guide to get and setup Racket 7.7 on your machine.

After you have successfully configured Racket, you'll to add Rosette (a solver-aided language) to the current Racket installation. In this homework, Rosette 3.2 is recommended. To install Rosette, first clone the Rosette repository:

```bash
git clone https://github.com/emina/rosette.git
```

Then checkout version 3.2:

```bash
cd rosette/
git checkout c092b65
```

And then install it from the source directly:

```bash
raco pkg remove rosette
raco pkg install
```

Then the environment for Venti should be ready.

## Problem Overview

You will be verifying smart contracts written by Solidity. A smart contract is a self-executing contract with the terms of the agreement between buyer and seller being directly written into lines of code. You can think of a smart contract as a special kind of source code that runs on a distributed and decentralized blockchain network, while the grammar of Solidity should look familiar if you used to write codes in C/C++/Java.

Even if you are not familiar with Solidity, we are not using/verifying any fancy features of Solidity itself; instead, the verification tasks here are relatively general.

## Problem 1 (40%): Test the Environment

First get Venti from github and check out the branch for homework `CS190I`:

```bash
git clone https://github.com/chyanju/Venti.git
cd Venti/
git checkout CS190I
```

And change directory to `targets/yul-ast-0.7.3` (without further notifications, we'll be using this client in this homework, and "working directory" refers to `targets/yul-ast-0.7.3` if not otherwise specified):

```bash
cd targets/yul-ast-0.7.3
```

So we'll be verifying the equivalence between two contracts: `P1A.sol` and `P1B.sol` in the `tests` folder under the working directory. Then, compile two smart contracts into YUL representations (for details of YUL language, see [here](https://docs.soliditylang.org/en/v0.7.3/yul.html) if you are interested):

```bash
solc ./tests/P1A.sol --ir --overwrite -o ./tests/
solc ./tests/P1B.sol --ir --overwrite -o ./tests/
```

Here ideally you should only see something like:

```
Compiler run successful. Artifact(s) can be found in directory ./tests/.
```

And this will give you `P1A.yul` and `P1B.yul` respectively in `tests` folder under the working directory. If you see something else rather than a successful message, one of your previous steps could have failed. Please revisit to correct it.

Next we pare the YUL files into json representations that are readable by the verifier:

```bash
python ./yul_parser.py --yul ./tests/P1A.yul
python ./yul_parser.py --yul ./tests/P1B.yul
```

You'll then see `P1A.json` and `P1B.json` from the `tests` folder under the workin directory, if everything works as expected. 

Then we can lanunch Venti to verify the equivalence between these two contracts using an existing configuration file `P1-config.json` in `configs` folder: 

```bash
racket ./yul-bmc.rkt --config ./configs/P1-config.json --verbose
```

If it runs successfully, you will see the following output:

```
task 0: #f
task 1: #t
```

#### Task 1-1 (20%)

Save your commands and their corresponding outputs into a file called `task1-1.txt`.

#### Task 1-2 (20%)

By observing the two contracts `P1A.sol` and `P1B.sol`, **<u>*briefly*</u>** explain whether the functions `modifyX` have the same semantics or not. If not, provide a counterexample input to these two functions where one returns a different output compared with the other. Write down your answer to a file called `task1-2.txt`.

## Problem 2 (60%): Customize the Verification Tasks

#### Venti Verification Design

In this homework, we define the notion of equivalence based on a special kind of functions, which we call `observe` functions. For example, in `P1A.sol` and `P1B.sol` there are identical `observe` functions that returns the same variable from the contract that we are trying to check equivalence of:

```java
function observe() public view returns (uint obsX) {
	obsX = xValue;
}
```

The `observe` functions are usually attached to a sequence of operations (i.e. function calls, as you can see in `Tasks` field of `P1-config.json`) to get the final value of the variables of interest. Then our client checks the equivalence of the two returned values (could be concrete or symbolic). You can think of this is a special kind of equivalence called "equivalence modulo observation".

For example, there are two tasks (or transactions) defined in `P1-config.json`, where each task is represented by a list of function calls. The first task:

```json
[
  [
  	"txn_function_call",
  	"constructor"
  ],
  [
  	"txn_function_call",
  	"observe"
  ]
]
```

calls the `constructor` first and then directly the `observe` function. The second task:

```json
[
  [
  	"txn_function_call",
  	"constructor"
  ],
  [
  	"txn_function_call",
  	"modifyX",
  	"uint"
  ],
  [
  	"txn_function_call",
  	"observe"
  ]
]
```

calls an additional method `modifyX` with corresponding argument of type `uint` (which will be initialized as a symbolic integer in Rosette) before calling the `observe` function.

#### Add a New Verification Task

In this problem, you are given two new smart contracts: `P2A.sol` and `P2B.sol`, which are slightly different from the ones provided in Problem 1, with additional class members and functions that deal with variable `yValue`. There's also a `P2-config.json` provided.

However, when you try to verify the equivalence of two smart contracts by following the aforementioned steps, you get the results saying the two contracts are equivalent, beause the returned results of every task from the two smart contracts are equal, which is **<u>*problematic*</u>** because the two smart contracts are not equal.

#### Task 2-1 (20%)

Read the smart contracts `P2A.sol` and `P2B.sol`, and **<u>*briefly*</u>** explain why they are not equivalent. Write down your answer to a file called `task2-1.txt`.

#### Task 2-2 (20%)

According to your manual analysis of the smart contracts from task 2-1 and understanding of the usage of `P1-config.json`, add additional task(s) to `P2-config.json` so that the verification tasks can capture the parts that are not equivalent of the two contracts, and output `#f` for that task. Submit the upated version of `P2-config.json`.

#### Task 2-3 (20%)

By default, Solidity initialize an integer to `0` if no initial value is given. If you include `constructor` function in any of your task definitions, can you still design `P2-config.json` to derive a `#f` result for some task to reveal the inequivalence of the two smart contracts? If yes, provide that new configuration file (and name it as `task2-3.json`); if no, **<u>*briefly*</u>** write down the reason in a file called `task2-3.txt`.

## 🤠 Problem 3 (0%): Write Your Own Client

Even though we here use the notion of "equivalence module observation", what Venti actually provides is a symbolic virtual machine for running YUL source code. Read the main entrance of this homework `yul-bmc.rkt` about how to create and manipulate symbolic virtual machines, and come up with your own client that defines and checks the equivalence in different ways other than using `observe` functions, e.g., checking all resulting memory locations of the two smart contracts.