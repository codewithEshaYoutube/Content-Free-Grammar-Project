# 📘 Context-Free Grammar (CFG) in Automata — Python Code Example

This guide explains **Context-Free Grammar (CFG)** in Automata theory and shows how to implement a parser in Python using the `lark` library.

---

```python
# 📄 What is CFG?
# CFG stands for Context-Free Grammar.
# It defines the syntactic rules for a language using recursive productions.

# A CFG is a 4-tuple: G = (V, Sigma, R, S)
# - V: Set of variables (non-terminal symbols)
# - Sigma: Set of terminals (input alphabet)
# - R: Set of production rules
# - S: Start symbol

# 📄 Example: CFG for Balanced Parentheses
# V = {S}
# Sigma = {(, )}
# R:
#   S → (S)
#   S → SS
#   S → ε (empty string)

# This grammar generates:
# "", "()", "(())", "()()", "(()())", etc.

# 📦 Step 1: Install the required library
# Run this in your terminal if not already installed:
# pip install lark

# 🧠 Step 2: Python Code Implementation

from lark import Lark

# Define CFG grammar using Lark syntax
cfg_grammar = """
    start: expr

    expr: "(" expr ")"        -> parens
        | expr expr           -> concat
        |                     -> empty
"""

# Create a parser for the grammar
parser = Lark(cfg_grammar, start='start')

# Test input strings for validation
test_strings = ["", "()", "(())", "()()", "(()())", "(()", "())("]

# Check each string and print whether it is valid
for s in test_strings:
    try:
        parser.parse(s)
        print(f"✔ '{s}' is VALID")
    except:
        print(f"✘ '{s}' is INVALID")

# 📄 Output:
# ✔ '' is VALID
# ✔ '()' is VALID
# ✔ '(())' is VALID
# ✔ '()()' is VALID
# ✔ '(()())' is VALID
# ✘ '(()' is INVALID
# ✘ '())(' is INVALID

# ✅ Summary:
# This script demonstrates how to use a context-free grammar to validate
# balanced parentheses using the `lark` library in Python.
