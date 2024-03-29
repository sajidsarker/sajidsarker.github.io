---
layout: post
title: NEO Linear Algebra for Python
date: 2022-09-10 16:22:28
tags: [Mathematics, Open Source, Python]
---
## NEO Linear Algebra for Python

**NEO Linear Algebra**<sup>[[1]](https://github.com/sajidsarker/neolinearalgebra)</sup> is a lightweight Python package designed for matrix operations in Linear Algebra programmed from scratch with Python. It does not employ any other package libraries to ammeliorate classes and methods with advanced functionality.

I built **NEO Linear Algebra** using *Object Oriented Programming* (OOP) architecture when designing the primary class for matrices.

The latest build (at time of writing) is **neolinearalgebra 0.2.4**<sup>[[2]](https://pypi.org/project/neolinearalgebra/0.2.4/)</sup> and can be installed using Python's *pip* package manager easily.

```bash
python3 -m pip install neolinearalgebra
pip install neolinearalgebra
```

### Motivation and *The Matrix*

I was inspired to program this package as part of a light review of the absolute fundamentals of Linear Algebra. Though I use this branch of mathematics heavily in my line of work with the popular *NumPy* and *Pandas*, I thought it would be a valuable exercise to implement skills I had already acquired in the development of a Python package for open source.

My motivation was not necessarily to produce an open source package to supplant or extend *NumPy*, but merely to learn and practice the development of fundamental software functionality I was already employing in industry tools. My hopes is that my work will aid Python beginners in the field of mathematics, statistics, economics, or engineering to have a complete and well-documented example available in the form of my work to learn from.

I was also inspired by my recent rewatch of the entirety of *The Matrix* quadrilogy. While the fourth film is not on par with the initial trilogy, it did have fascinating takes on the future of AI, robotics, and virtual constructs mimicking human forms and human intelligence.

### Goals and Constraints

My personal constraints and goals for this project included the following:
1. Build a lightweight mathematics library
2. Apply OOP architecture in class design
3. Restrict myself to Python 3.10 for package development
4. Rely only on built-in Python data structures (e.g. lists, dicts etc.)
5. No advanced package functionality; not be a wrapper for another package
6. Open source under MIT license
7. Modular design for future extensibility
8. Produce a minimum viable product
9. Generate comprehensive documentation of my code for easy review
10. Create comprehensive unit tests for my code for debugging
11. Deploy my package to *PyPI*

Given I had made the decision to make my work open source, and knowing full well I will never be able to compete with *NumPy*, I felt the best course of action would be to create a minimum viable product, host a development repository on *Github* for public forking, and focus on simplicity, quality of syntax, and comprehensive documentation<sup>[[3]](/docs/assets/documentation/neolinearalgebra/Documentation.html)</sup>.

With my choice of Linear Algebra and love for *The Matrix*, I decided to write a singular *Matrix* class. Matrix manipulation and operations I envisioned at first included:
- Integrity Checks
- Addition
- Subtraction
- Scalar Multiplication
- Pointwise Multiplication
- Matrix Multiplication (Dot Product)
- Transposition
- Diagonalisation
- Trace
- Determinant
- Inversion
- Magnitude
- Sum
- Mean

What I ended up with is something very clean and intuitive!

```python
A = Matrix([[1, 0], [0, 1]])
B = Matrix([[1, 0, 0], [0, 1, 0], [0, 0, 1]])
C = Matrix([[10, 9, 7], [6, 5, 4], [3, 2, 1]])

A + A
'''
<class: 'Matrix'>
Dimensions: 2 row(s) x 2 column(s)
 [[2, 0],
  [0, 2]]
Size: 4 element(s), 136 byte(s)
'''

B * C   # Pointwise Multiplication
'''
<class: 'Matrix'>
Dimensions: 3 row(s) x 3 column(s)
 [[10, 0, 0],
  [0, 5, 0],
  [0, 0, 1]]
Size: 9 element(s), 136 byte(s)
'''

B @ C   # Matrix Multiplication
'''
<class: 'Matrix'>
Dimensions: 3 row(s) x 3 column(s)
 [[10, 9, 7],
  [6, 5, 4],
  [3, 2, 1]]
Size: 9 element(s), 136 byte(s)
'''

B.inverse().transpose()
'''
<class: 'Matrix'>
Dimensions: 3 row(s) x 3 column(s)
 [[1.0, 0.0, 0.0],
  [0.0, 1.0, 0.0],
  [0.0, 0.0, 1.0]]
Size: 9 element(s), 136 byte(s)
'''
```

### Tools and Workflows
My workflow involved writing a series of unit tests first, which I would run as a whole each time I had completed a feature or individual method.

I tested specifically for expected operation of the class methods, and also the properties of matrices in Linear Algebra:
- Commutativity
- Associativity
- Distributivity
- Identity

Tools I used were pretty humble:
- Git
- Vim
- Jupyter Notebook

Python packages I used:
- unittest: Unit testing
- pdoc: Documentation

### Future Extensibility

After deployment, I hope to update functionality of my package by extending the Matrix class as the parent for a new Vector class (a special case of matrices), and extend it to functions such as:
- Normal
- Cross Product

### Open Source

[[1] NEO Linear Algebra Open Source on Github](https://github.com/sajidsarker/neolinearalgebra)

[[2] neolinearalgebra 0.2.4 - PyPi.org](https://pypi.org/project/neolinearalgebra/0.2.4/)

[[3] NEO Linear Algebra Documentation](/docs/assets/documentation/neolinearalgebra/Documentation.html)
