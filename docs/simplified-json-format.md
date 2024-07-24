### Complete JSON Mappings with Simplifications and Explanations

1. **Literal**
    - **Explanation:** Represents a literal value like 13, True, or "foo".
    ```json
    {
      "Literal": {
        "type": "LiteralType",
        "value": "literalValue"
      }
    }
    ```

2. **Constructor**
    - **Explanation:** Reference to a custom type constructor name. If the type constructor has arguments, this node will be wrapped into some `Apply` nodes depending on the number of arguments.
    ```json
    {
      "Constructor": {
        "name": "constructorName",
        "args": ["arg1", "arg2", ...]
      }
    }
    ```

3. **Tuple**
    - **Explanation:** Represents a tuple value. Each element of the tuple is in turn a `Value`.
    ```json
    {
      "Tuple": {
        "elements": ["elem1", "elem2", ...]
      }
    }
    ```

4. **List**
    - **Explanation:** Represents a list of values. Each item of the list is in turn a `Value`.
    ```json
    {
      "List": {
        "items": ["item1", "item2", ...]
      }
    }
    ```

5. **Record**
    - **Explanation:** Represents a record value. Each field value of the record is in turn a `Value`.
    ```json
    {
      "Record": {
        "fields": {
          "fieldName1": "fieldValue1",
          "fieldName2": "fieldValue2"
        }
      }
    }
    ```

6. **Variable**
    - **Explanation:** Reference to a variable.
    ```json
    {
      "Variable": {
        "name": "variableName"
      }
    }
    ```

7. **Reference**
    - **Explanation:** Reference to another value within or outside the module. References are always fully-qualified to make resolution easier.
    ```json
    {
      "Reference": {
        "fqName": "fullyQualifiedName"
      }
    }
    ```

8. **Field**
    - **Explanation:** Represents accessing a field on a record together with the target expression. This is done using the dot notation in Elm: `foo.bar`.
    ```json
    {
      "Field": {
        "subject": "subjectValue",
        "fieldName": "fieldName"
      }
    }
    ```

9. **FieldFunction**
    - **Explanation:** Represents accessing a field on a record without the target expression. This is a shortcut to refer to the function that extracts the field from the input. This is done using the dot notation in Elm without a target expression: `.bar`.
    ```json
    {
      "FieldFunction": {
        "fieldName": "fieldName"
      }
    }
    ```

10. **Apply**
    - **Explanation:** Represents a function application. The two arguments are the target function and the argument. Multi-argument invocations are expressed by wrapping multiple `Apply` nodes in each other (currying).
    ```json
    {
      "Apply": {
        "function": "functionValue",
        "arg": "argumentValue"
      }
    }
    ```

11. **Lambda**
    - **Explanation:** Represents a lambda abstraction. The first argument is a pattern to match on the input, the second is the lambda expression's body.
    ```json
    {
      "Lambda": {
        "argumentPattern": "pattern",
        "body": "bodyValue"
      }
    }
    ```

12. **LetDefinition**
    - **Explanation:** Represents a single let binding. Multiple let bindings are achieved through wrapping multiple let expressions into each other.
    ```json
    {
      "LetDefinition": {
        "name": "nameValue",
        "definition": "definitionValue",
        "in": "bodyValue"
      }
    }
    ```

13. **LetRecursion**
    - **Explanation:** Special let binding that allows mutual recursion between the bindings. This is necessary because `LetDefinition` will not make recursion possible due to its scoping rules.
    ```json
    {
      "LetRecursion": {
        "definitions": {
          "name1": "definition1",
          "name2": "definition2"
        },
        "in": "bodyValue"
      }
    }
    ```

14. **Destructure**
    - **Explanation:** Applies a pattern match to the first expression and passes any extracted variables to the second expression. This can be represented as a let expression with a pattern binding or a single-case pattern-match in Elm.
    ```json
    {
      "Destructure": {
        "pattern": "destructPattern",
        "value": "valueToDestruct",
        "body": "bodyValue"
      }
    }
    ```

15. **IfThenElse**
    - **Explanation:** Represents a simple if/then/else expression. The 3 arguments are: the condition, the then branch, and the else branch.
    ```json
    {
      "condition": "conditionValue",
      "then": "thenBranchValue",
      "else": "elseBranchValue"
    }
    ```

16. **PatternMatch**
    - **Explanation:** Represents a pattern-match.
    ```json
    {
      "PatternMatch": {
        "match": "matchValue",
        "cases": [
          {
            "pattern": "pattern1",
            "body": "body1"
          },
          {
            "pattern": "pattern2",
            "body": "body2"
          }
        ]
      }
    }
    ```

17. **UpdateRecord**
    - **Explanation:** Expression to update one or more fields of a record. As usual in FP, this is a copy-on-update so no mutation is happening.
    ```json
    {
      "UpdateRecord": {
        "record": "recordValue",
        "updates": {
          "fieldName1": "newValue1",
          "fieldName2": "newValue2"
        }
      }
    }
    ```

18. **Unit**
    - **Explanation:** Represents the single value in the Unit type. When you find Unit in the IR, it usually means: "There's nothing useful here".
    ```json
    {}
    ```

