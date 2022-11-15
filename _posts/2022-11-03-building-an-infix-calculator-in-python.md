---
layout: post
title: Building an Infix Calculator in Python
date: 2022-11-03 00:01:02
tags: [Python, Mathematics, Open Source]
---
## Building an Infix Calculator in Python

### Motivation

When writing mathematical expressions, we generally utilise what is known as infix notation. In infix form, an operator is written in between the two operands on which the operation is to be evaluated.

Evaluation of these operators is then in the order of **PEMDAS**:
1. Parentheses
2. Exponents
3. Multiplication
4. Division
5. Addition
6. Subtraction

Given that the computer is naive, we must resort to alogithmically evaluating a mathematical infix expression by converting it first into either postfix or prefix notation which is easier for a computer to process systematically.

My code for a CLI infix calculator `calculator.py` takes an infix expression as a string at runtime in the terminal from where it is called, performs validation checks to ensure that it is a valid infix expression, algorithmically converts it into a postfix expression, then evaluates the postfix expression to yield the correct answer.

The source code for this project is available on my Github<sup>[[1]](https://github.com/sajidsarker/infix-calculator)</sup> for both personal use and as an educational sample under the MIT license.

### Source Code

```python
#!/usr/bin/python3

import sys

def compareOperations(operation, target):
    if operation == "^":
        return True
    if operation == "*":
        if target == "^":
            return False
        else:
            return True
    elif operation == "/":
        if target == "*" or target == "^":
            return False
        else:
            return True
    elif operation == "+":
        if target == "+" or target == "-":
            return True
        else:
            return False
    else:
        return False

class InfixExpression:
    infix = []
    operands = []
    operators = []

    def __init__(self, infixexpression):
        operations = ["+", "-", "*", "/", "^"]
        
        for character in infixexpression:
            if character not in operations and (character == "." or character.isnumeric()):
                
                if len(self.infix) - 1 < 0:
                    self.infix.append(character)
                else:
                    self.infix[len(self.infix)-1] += character
                    
            elif character in operations:
                
                if len(self.infix) - 1 < 0:
                    self.infix.append(character)
                    
                elif self.infix[len(self.infix)-1] in operations or self.infix[len(self.infix)-1] == "":
                    
                    if self.infix[len(self.infix)-1] == "-":
                        self.infix.append(character)
                    else:
                        self.infix[len(self.infix)-1] += character
                        
                    if character != "-":
                        self.infix.append("")
                        
                else:
                    self.infix.append(character)
                    self.infix.append("")

        if self.infix[len(self.infix)-1] == "":
            self.infix.pop(-1)

        if self.check_infix() == False:
            print("Error: Invalid infix expression!")

        #print("Infix Expression:", self.infix)

        return None

    def check_infix(self):
        operations = ["+", "-", "*", "/", "^"]

        for element in self.infix:
            if element not in operations:
                self.operands.append(element)
            elif element in operations:
                self.operators.append(element)

        if len(self.operands) == 0 and len(self.operators) == 0:
            return True

        if len(self.operands) > 0 and len(self.operators) == 0:
            return True

        if len(self.operands) == 0 and len(self.operators) > 0:
            return False

        if len(self.operands) <= len(self.operators) and self.infix[0] != "-":
            return False
        elif self.infix[0] == self.operators[0] and self.infix[0] != "-":
            return False
        elif self.infix[len(self.infix)-1] == self.operators[len(self.operators)-1]:
            return False
        else:
            operations = ["+", "-", "*", "/", "^"]
            i = 0
            while i < len(self.infix)-1:
                if self.infix[i] in operations and self.infix[i+1] in operations:
                    return False
                i += 1
            return True

    def infixtopostfix(self):
        operations = ["+", "-", "*", "/", "^"]
        buffer = []

        self.operands = []
        self.operators = []

        for element in self.infix:
            if element not in operations:
                buffer.append(element)
            elif element in operations:
                thisOps = element
                while self.operators != [] and compareOperations(self.operators[-1], thisOps) == True:
                    buffer.append(self.operators.pop(-1))
                self.operators.append(thisOps)

        while self.operators != []:
            buffer.append(self.operators.pop(-1))
        
        print("Postfix Expression:", buffer)
        
        return buffer

    def evaluate(self):
        operations = ["+", "-", "*", "/", "^"]

        self.operands = []
        self.operators = []
        
        for element in self.infix:
            if element not in operations:
                self.operands.append(element)
            elif element in operations:
                thisOps = element
                while self.operators != [] and compareOperations(self.operators[-1], thisOps) == True:
                    o = self.operators.pop(-1)
                    b = self.operands.pop(-1)
                    a = self.operands.pop(-1)
                    a, b = float(a), float(b)
                    if o == "^":
                        self.operands.append(a**b)
                    elif o == "*":
                        self.operands.append(a*b)
                    elif o == "/":
                        self.operands.append(a/b)
                    elif o == "+":
                        self.operands.append(a+b)
                    elif o == "-":
                        self.operands.append(a-b)
                self.operators.append(thisOps)
            
        while self.operators != []:
            o = self.operators.pop(-1)
            b = self.operands.pop(-1)
            a = self.operands.pop(-1)
            a, b = float(a), float(b)
            if o == "^":
                self.operands.append(a**b)
            elif o == "*":
                self.operands.append(a*b)
            elif o == "/":
                self.operands.append(a/b)
            elif o == "+":
                self.operands.append(a+b)
            elif o == "-":
                self.operands.append(a-b)

        print("Evaluated:", self.operands)

        return self.operands

def main():
    if len(sys.argv) == 2:
        expression = str(sys.argv[1:])

        calculation = InfixExpression(expression)

        if calculation.check_infix() == False:
            sys.exit()
        else:
            calculation.infixtopostfix()
            calculation.evaluate()

    else:
        print('Error in expression. Please type "./calculator.py <expression>" or "python calculator.py <expression>" with the expression surrounded by quotation marks.')

if __name__ == '__main__':
    main()
```

### Open Source

[[1] Github Repository: Infix Calculator](https://github.com/sajidsarker/infix-calculator)
