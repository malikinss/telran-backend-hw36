# Homework 36 – LTR Arithmetic Expression Evaluator

## Task Definition

The goal of Homework 36 is to extend the **Left-to-Right (LTR) arithmetic evaluator** from CW #36 with additional validation and testing capabilities.

Specifically, the task requires:

1. Implementing a new method `check_arithmetic_expr` in `ExpressionValidator` which:
    - Validates arithmetic expressions against a **regex-based syntax**,
    - Ensures proper placement of operands (integers or floats) and operators,
    - Supports all operators defined in `OperatorRegistry`, including `**` (power),
    - Checks **parentheses pairing** (only round brackets `()`),
    - Notes:
        - Regex can check the syntax of parentheses but **cannot verify pairing**,
        - Parentheses pairing logic checks that every opening bracket is matched with a closing bracket in the correct order.

    Examples:

    ```py
    # Syntax OK but parentheses unpaired
    "(10 + 20))))"  # passes regex but fails pairing
    # Paired parentheses but invalid syntax
    "() + 10 (/) 20"  # fails regex
    ```

2. Writing **additional unit tests** to verify:
    - Syntax correctness of expressions,
    - Proper pairing of parentheses,
    - Edge cases including nested parentheses, whitespace, invalid tokens.

---

## 📝 Description

This project implements a **Left-to-Right arithmetic expression calculator** in Python that evaluates expressions **strictly in the order operators appear**, ignoring classical operator precedence.

The calculator is capable of:

- Handling nested parentheses via recursive evaluation,
- Validating **expression syntax** against allowed numeric formats and operators,
- Checking **parentheses pairing** using a stack-based approach,
- Delegating actual arithmetic computation to a dedicated evaluation layer (`LeftToRightEvaluator`).

The project structure:

```
./src/
 ├─ ltr.py                 # Main LTR calculator
 ├─ evaluation/            # Left-to-right evaluator and operator registry
 ├─ regex/                 # Expression regex patterns and validators
 └─ utils/                 # Parentheses checker and utility functions

./tests/
 ├─ test_ltr_evaluation.py # LTR calculator tests
 └─ test_regex.py          # Regex and parentheses validation tests
```

---

## 🎯 Purpose

The homework focuses on:

1. **Algorithmic correctness** – Ensuring that arithmetic expressions are evaluated correctly in a strict left-to-right order, regardless of operator precedence.
2. **Input validation** – Providing a robust mechanism to catch malformed expressions before evaluation.
3. **Error handling** – Detecting unbalanced parentheses, invalid operators, and division by zero.
4. **Python best practices** – Using type annotations, docstrings, modular code, and unit testing.

By combining regex-based syntax validation and stack-based parentheses checking, the project ensures safe and predictable expression evaluation.

---

## 🔍 How It Works

1. **Validation**
    - Parentheses pairing is checked using `ParenthesesChecker`.
    - Syntax validation is performed using `ExpressionValidator` with regex patterns generated from `OperatorRegistry`.

2. **Whitespace removal**
    - All spaces in the expression are removed to simplify parsing.

3. **Recursive parentheses evaluation**
    - Innermost parentheses are evaluated first.
    - Each subexpression is replaced with its computed numeric value.

4. **Left-to-right evaluation**
    - Once all parentheses are resolved, the expression is evaluated strictly left-to-right using `LeftToRightEvaluator`.
    - Operators are applied sequentially, ignoring conventional precedence rules.

5. **Error propagation**
    - `ValueError` is raised for invalid syntax,
    - `ZeroDivisionError` is propagated when division by zero occurs.

---

## 📜 Output Example

### ✅ Valid expression

```py
expr = "(3 + (2 * 10 / (40 - 20)) + (3 * 4)) * 10"
calculator.evaluate(expr)
# → 160.0
```

### ❌ Invalid syntax

```py
expr = "4 + 2   5"
calculator.evaluate(expr)
# → ValueError
```

### ❌ Division by zero

```py
expr = "4 + 2 / (20 / 20 - 1)"
calculator.evaluate(expr)
# → ZeroDivisionError
```

### ❌ Unbalanced parentheses

```py
expr = "((3+2) + 5"
calculator.evaluate(expr)
# → ValueError
```

---

## 📦 Usage

```py
from src.ltr import LtrCalculator

calculator = LtrCalculator()

expr = "((3 + 2) * 4) / 2"
result = calculator.evaluate(expr)
print(result)  # Output: 10.0
```

### Running Tests

```bash
python -m unittest discover -s tests
```

All tests validate:

- Regex-based syntax validation,
- Parentheses pairing,
- Correct evaluation of left-to-right expressions,
- Handling of floating-point numbers and operators.

---

## ✅ Dependencies

- Python 3.10+
- Standard library only (`re`, `unittest`, `typing`)

---

## 📊 Project Status

**Status:** ✅ Completed

- All unit tests pass successfully.
- Supports nested parentheses and all operators defined in `OperatorRegistry`.
- Robust against syntax errors and division by zero.

---

## 📄 License

MIT License

---

## 🧮 Conclusion

This project demonstrates a **modular, test-driven approach** to building a custom arithmetic evaluator in Python.

Key takeaways:

- Regex and stack-based validation can complement each other for **safe input parsing**,
- Left-to-right evaluation requires careful orchestration of operands and operators,
- Unit testing ensures reliability across a wide range of valid and invalid expressions.

---

Made with ❤️ and `Python` by **Sam-Shepsl Malikin** 🎓
