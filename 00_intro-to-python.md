---
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.1'
      jupytext_version: 1.1.0
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

# Lab 00 - Introduction to Python and Jupyter Notebooks

**Author**: Kenneth Wong (kennethwong12.netlify.app)

**Last Edited**: 2021-10-25

---

## Setup

```python
!pip3 install numpy pandas matplotlib
```

---

This session will cover the basics of Python, and introduce elements that will help you get familiar with Python as an interactive computational environment for exploring data. The material is presented in an interactive environment that runs within your web browser, called a Jupyter Notebook.  It allows presentation of text and graphics to be combined with Python code that can be run interactively, with the results appearing inline.  We are looking at a Jupyter notebook now.  Note that Jupyter is a relatively recent name for this so sometimes you may still see it referred to as an IPython noteboook.  Jupyter is just the new version of IPython notebooks, but now also supports a variety of other languages and tools.

If you click on this entry in the directory within the Jupyter Notebook, another tab will be created in your browser, containing this notebook, ready to use.  Go ahead and do that.

Note that it has cells, that contain text (until farther down in the notebook). These are markdown cells. Notice the pulldown list for the cell type contains:

- Code -- which we will use for Python code mainly, though it could use other languages
- Markdown, like this cell, using a flavor of structured text like that used in Wikipedia and many other platforms
- Other options will appear depending on what else is installed for use with Jupyter, like kernels for Scala, R, Octave, etc.

You can edit the contents of a cell by double-clicking on it.  Try it on this cell.

When you are ready to save it or exit edit mode, just use `Shift + Enter`.

We will see how the code cells work next, in the context of learning a bit about the Python programming language.

Before going on to that, though, just note that you can use Markdown syntax to format your text.  Documentation on the markdown syntax is available here: http://jupyter-notebook.readthedocs.io/en/latest/examples/Notebook/Working%20With%20Markdown%20Cells.html

Cells can also contain programs, or code.  We will be using Python code extensively in this course.  The next cell contains a Python command, and that command can be executed in the Notebook by clicking Shift-Enter on the cell, or selecting Cell/Run Cells from the menu, or clicking on the Run icon  (left of the black square), on the toolbar.  Notice that it executes the command and writes the output below the cell.

---

## Python

Python is an interpreted programming language, also referred to as a high-level language, or as a scripting language.  What this means is that when you write some commands, or statements that are meaningful in the Python language, the Python 'interpreter' reads the command, figures out what the intended computation is, and then executes it.  This differs from low-level languages like C or C++, in which you generally have to compile code  before you can run it, and if you find errors they have to be diagnosed and then the code re-compiled before you can run it.  Interpreted languages skip the compile step, and just execute code directly, and if there are errors, they are seen at run-time. 

### Python Interpreter Environments

When we write and execute Python code, we generally do that within an environment known as an Interpreter. Python interpreter and editing environments can be quite varied. Some options include:

1. Starting Python at the command line, by typing 'python' at the command prompt (c:\ on windows, for example)
1. Starting an editor that can edit and run Python, like Idle, which comes built-in with Python,or programming editors like Scite.
1. The way we will generally interact with Python is through Juoyter Notebooks like this one, that provide a Python environment that runs in your web browser.  This is the environment you are looking at now, with a mixture of headings, text, and code embedded in a Jupyter Notebook.

---

## Hello World!

The first programming command demonstrated when you are learning a programming language is usually to make the computer print 'Hello World!'.  In Python, doing this is pretty simple:

```python
print("Hello World!")
```

As you can see, there is not much code involved in making this happen.  The word `print` is a command that Python knows how to process, and the text string 'Hello World!' in quotations is an *argument* being passes to the print command.  You can of course pass any kind of argument to the Python print command, and it will try to *do the right thing* without you having to micro-manage the process.

## Python as an Interactive Calculator

Something 

```python tags=["parameters"]
param = 5
```

Python can be used as a simple interactive calculator, by just typing in a mathematical expression as you might on a regular or scientific calculator:

```python
2 + 2
```

What happened above is that Python interpreted the line '2+2' to parse that it should understand the first object it encountered as an integer, the second object as a mathematical operator for addition, and the third as another integer.  Python's interpreter mostly just tries to figure out what you mean when you write statements like this, and as long as it is unambiguous and feasible to compute, it just does it without you having to explain things in detail.

---

## Importing packages

Packages are collections of pre-written code made available for reuse. In the previous lesson, we installed some necessary packages using the `pip3` python package manager. Packages are convenient because they save you from having to implement every feature and function on your own. The widely-used packages also provide a standard, common set of tools for others to develop with --- allowing interoperability between programs.

There are a few different ways to import package in python:

The simplest is just to `import {packagename}`. For this lesson, we'll use `numpy` as the example package

```python
import numpy
```

The functions, classes, and variables of the `numpy` package can then be accessed using "dot" notation: for example, the numpy array class can be accessed with `numpy.array`

A variant of this is to use `import {packagename} as {shortname}`, as in:

```python
import numpy as np
```

This reduces the number of characters needed to type, and can be convenient if the package name is long, or you need to use many things from the same package. Accessing the numpy array class, for example, can be done with `np.array`


## The Pylab Interactive Plotting Environment

OK, so maybe using Python as an interactive calculator is not the most compelling case for using Python, even if it does demonstrate that Python has a very shallow learning curve for someone completely new to programming.  You can actually begin using it productively even before learning how to program in it!

To give a preview of somewhat more advanced topics, let's look at the interactive plotting mode in IPython that we can invoke by using 'magic' commands, and importing some modules: 

```python
#magic command to display matplotlib plots inline within the Jupyter notebook webpage
%matplotlib inline
#import necessary modules
import pandas as pd, numpy as np, matplotlib.pyplot as plt
```

(See the [magic function documentation](https://ipython.readthedocs.io/en/stable/interactive/tutorial.html#magic-functions) of IPython to understand more about it)

This loads pandas and numpy and the matplotlib plotting environment.  We'll come back to these libraries in more detail later, but now let's look at how they allow us to extend the range of things we can do.  Let's assign 1,000 sequential numbers to a variable labeled x, and create another variable, y, that has some transformation of x, and then plot y against x:

```python
x=range(100)
y=np.sin(x)
plt.plot(x*y)
```

---

## Data Type

Data in Python is interpreted as having a **type**.  In low-level, compiled languages like C or C++, the programmer has to explicitly declare the type of each variable before actually using it.  In Python, the type is inferred at run time, and you can always ask Python what the type of an object is with `type()` function:

```python
a = 13
print (type(a))
```

```python
a = a*1.1
print (type(a))
```

```python
a = 'Hello World!'
print (type(a))
```

Notice that when we multiply a, which was initially an integer, by a floaring point (decimal number) the result is **cast** as a float.  This is like the integer divide problem earlier -- using a floating point number in the calculation causes the result of the calculation to become a floating point number.

Notice also that we can reassign any value or type to a variable.  We began with **a** being an integer, then changed its value to a float, and then to a string (text).  Variables are dynamically updated in this way based on values assigned to them.

---

## Python Scripts

All the examples we have typed in to the Jupyter Notebook have been statements  evaluated interactively as soon as we type them and execute them with a Shift-Enter.  While this is an excellent way to develop confidence in learning Python, and later for interactively exploring data, it is also often useful or necessary to store statements in a Python script that can be rerun at any time.

Python scripts are just text files stored on disk, containing Python statements and comments.  The convention of using **.py** as the suffix for a Python script makes it easy to find and run such scripts and to have the Python interpreter parse the statements and execute them one at a time, from top to bottom, as though they had been entered interactively (there are some minor differences in how the interpreter parses interactive commands as compared to scripts, but we will ignore that for now).

Comments are a good thing to add to scripts to provide some documentation of what the script is supposed to do, or how to use the script, or to remind yourself later what you had in mind when you wrote the script.  The convention is to use a # sign at the beginning of the line to indicate that that line is a comment, and not to be parsed and executed by Python.  It does not significantly slow down Python to have to step through comments and ignore them -- so use comments liberally!

```python
# This is a comment explaining the code below
# which I would not remember in detail later without comments
income = 50000.0+10000*np.random.randn(10)
y = np.log(income)
y
```

You can import and export Python scripts from the IPython Notebook.  Once you have a notebook you want to save as a Python script, you can select 'File', 'Download as', and then 'Python (.py)'.  This will save the code as a Python script that can be reloaded in a Notebook or executed in **Batch** mode, or run from beginning to end sequentially, without waiting for you to execute each cell one by one.

Python scripts can be run at the command line by typing python and then the name of the python script you want to run, as in: **c:\python test.py**. They can also be loaded into an IPython session, such as into a Notebook, and run there.

