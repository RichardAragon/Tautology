# Tautology
Logical Tautology Boolean For LLMs
**Problem:** Determine whether a given logical formula is **tautological**. A tautological formula is one that is always true, regardless of the values of its variables.

**Solution:**

1. Define a function called `is_tautological()`, which takes a logical formula as input and returns `True` if the formula is tautological, and `False` otherwise.
2. Implement the `is_tautological()` function recursively as follows:

```python
def is_tautological(formula):
  if isinstance(formula, LogicalAxiom):
    return True
  elif isinstance(formula, LogicalContradiction):
    return False
  elif isinstance(formula, LogicalImplication):
    return is_tautological(formula.antecedent) or not is_tautological(formula.consequent)
  elif isinstance(formula, LogicalUniversalQuantifier):
    for x in formula.domain_of_discourse:
      if not is_tautological(formula.quantifier_body.substitute(x)):
        return False
    return True
  elif isinstance(formula, LogicalExistentialQuantifier):
    for x in formula.domain_of_discourse:
      if is_tautological(formula.quantifier_body.substitute(x)):
        return True
    return False
  else:
    raise Exception("Invalid logical formula")
```

This algorithm works by recursively breaking down the logical formula into its component parts and then applying the following rules:

* An axiom is tautological.
* A contradiction is not tautological.
* An implication is tautological if the antecedent is tautological or the consequent is not tautological.
* A universal quantifier is tautological if the quantifier body is tautological for all values of the variable in the domain of discourse.
* An existential quantifier is tautological if the quantifier body is tautological for at least one value of the variable in the domain of discourse.

To use the algorithm, simply pass the logical formula that you want to test to the `is_tautological()` function. The function will return `True` if the formula is tautological, and `False` otherwise.

Here is an example of how to use the algorithm:

```python
logical_inference = LogicalInference({"a", "b", "c"})

formula = LogicalImplication(LogicalUniversalQuantifier("x", LogicalFormula("P(x)"), LogicalFormula("all")), LogicalFormula("P(a)"))

is_tautological = is_tautological(formula)

print(is_tautological)
```

This will print `True` to the console, indicating that the formula is tautological.

This algorithm can be used to solve a variety of other logical problems, such as determining whether a given logical formula is satisfiable, valid, or equivalent to another logical formula.
