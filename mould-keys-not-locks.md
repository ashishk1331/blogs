---
title: Mould keys not locks
slug: mould-keys-not-locks
pubDate: 2025-03-16
draft: true
description: How printing patterns can help you come up with better algorithms to solve tasks.
author: Ashish Khare
---

![banner](./assets/mould-keys-not-locks/banner.webp)

Last year, I solved about half of the _Advent of Code_ problems (I know, it sounds embarrassing 🥲), and I came across this interesting problem: [Day 24: Crossed Wires](https://adventofcode.com/2024/day/24).

In this problem, you are given a set of registers and a series of recursively dependent operations that use either the register values or the results of previous operations. _(Check the sample input on the problem page.)_ Our task was to identify values stored in registers starting with the name `z` and concatenate the results to form a whole number, which would be the answer.

You can pick any algorithm or pattern to solve this problem. However, I wanted to discuss a pattern called `Abstract Syntax Tree`. One might say it would be a overkill for a small problem like this. I'll reassure you, it isn't.

## Framing the Tree

```python
{
    'x00': {'type': 'var', 'value': 1},
    'x01': {'type': 'var', 'value': 1},
    'x02': {'type': 'var', 'value': 1},
    'y00': {'type': 'var', 'value': 0},
    'y01': {'type': 'var', 'value': 1},
    'y02': {'type': 'var', 'value': 0},
    'z02': {'type': 'fn', 'op': 'OR', 'params': ('x02', 'y02')},
    'z01': {'type': 'fn', 'op': 'XOR', 'params': ('x01', 'y01')},
    'z00': {'type': 'fn', 'op': 'AND', 'params': ('x00', 'y00')}
}
```

We can classify the given data into two formats: either it is a register value, referred to as `var`, or an operation, referred to as `fn`.

1.  **Variables**

    The basic syntax of a variable consists of two properties: `type` and `value`. The `value` property holds the value of the register or variable.

2.  **Operations**

    An `fn` type has three properties: `type`, `op`, and `params`. The `params` property holds the list of dependencies for that operation, while `op` differentiates the type of operation.

### Key Insights:

- Each token has a `type` property, which is used to distinguish between different tokens.
- The AST does not store any functionality or behavior within it. It only describes the structure and static values.

## Parsing the Tree

Once you've created an AST, you can parse it through code to generate values or perform operations. This is the part where you attach functionality to the AST and derive meaningful results.

```python
def part_one(inp):
    ops = {
        "AND": lambda x, y: x & y,
        "OR": lambda x, y: x | y,
        "XOR": lambda x, y: x ^ y,
    }

    def evaluate(wire):
        mode = inp[wire]

        if mode["type"] == "var":
            return mode["value"]
        else:
            return ops[mode["op"]](*map(evaluate, mode["params"]))

    res = 0
    for wire in inp:
        if wire.startswith("z"):
            index = int(wire[1:])
            res += evaluate(wire) * (2**index)

    return res
```

### Code Explained:

1. `inp` contains the instance of the AST.
2. `ops` stores all possible operations along with their corresponding lambda functions.
3. `evaluate()` is a function that recursively computes the values of all variables starting with _z_.

### Code Modifications:

There are several ways to extend this code to handle edge cases and improve fault tolerance and robustness:

1. The `ops` dictionary should contain references to functions that, in turn, should accept a variable number of positional arguments and handle empty scenarios.
2. The `evaluate()` function should implement memoization for both functions and parameter lists.

## Mid-Post Conclusion

This problem demonstrates the use of Abstract Syntax Trees and how they can help structure data into meaningful information. It also shows how code can be formulated to derive results from the syntax tree.

Oh yeah! The "Syntax" in AST might be confusing. You might be thinking, "Wait, the problem wasn't about programming language compilation. It was just a simple recursive problem, so why bring in AST?" It may seem like a wild theory at first, but its structure helps in organizing and evaluating the problem systematically.

Think of ASTs as a pencil box with dedicated sections for erasers, pencils, colors, and even stamps. You could always use a pouch or a bag to hold everything together, but having a pencil box helps segregate items more efficiently and provides you with the strongest probabilities of where to look for certain items in the box.

It also guarantees that the input shape remains fixed, so you don’t need to worry about anomalies or missing properties. Plus, it helps visualize the data more coherently and methodically.

## Bigger Example: TetraPack

[TetraPack](https://tetra-docs.vercel.app/) is one of my projects that helps you render Notion pages in your Next.js applications. It's useful for building blogs, documentation sites, and more.

It accepts data from the Notion API and converts it into an intermediate AST. Afterwards, it renders the AST onto the screen as vanilla HTML components.

You can try it out!

## Conclusion

I wanted you to see this tree pattern and how you can use it to solve problems of varying sizes—from a small coding challenge to building an npm library. Beyond language compilers, there are many other areas where this approach can be applied.

Have fun!
