### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```
For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).


## Introduction :dancer:
In his article “The Complexity of Dance Choreography Procedures”, Nigel Gwee seeks to define the complexity of dance choreography.

## Background Information
## Decision Problems
### Dance Choreography (DC)
Dance Choreography is the base problem for this proof that all following problems rely on. It is composed of the Instance, which specifies the components of the problem, and the Question, which specifies what the problem is.

**Instance**
```
A finite set of _Figures_;
a set _Follow_ of tuples <f-i, f-j>, f-i, f-j in _Figures_;
n in Natural Numbers;
_f-start_, _f-end_ in _Figures_;
a set _Compulsory_ that is a subset of _Figures_
```
### Hamiltonian Circuits (HC)
A Hamiltonian Circuit (HC) is a known NP-Complete problem on a graph which asks whether the graph includes a simple circuit containing all vertices. 

DC can be given certain parameters to create a HC:
- Set _Compulsory_ equal to _Figures_ so that the two sets contain all of the “vertices” 
- Set _f-start_ = _f-end_ so that DC ends where it starts and creates a circuit to fulfill the requirements of a HC

Since by restricting DC with these requirements we can convert it to a HC, it must also be NP-Complete.

### Dance Choreography k (DCk)


## Optimization Problems
We make the transition from decision problems to optimization problems with the help of the problem DCk, which is shown above. Rather than asking if the object of focus, a graph in this case, contains certain elements, optimization problems look to see if an optimum solution can be found and how hard it is to find it. 

Here optimization is based on set cardinality. In other words, the most optimum solution is that with the most variation in the figures. 
### Dance Choreography Optimization (DCO)
We show that DCO is NP-hard through showing that DCk, which is NP-complete, is Turing reducible to DCO''
```markdown
Let max be the optimal solution for an instance of DCO, where max = |{f1, .. fn}|. 
```
The Turing Machine would appear as the following:
```
For an instance of DCk:
  k ≤ max → yes 
  Else →  no
```
## Exhaustive and Heuristic Algorithms
Since we are talking about optimization, it is important to also talk about algorithms which help us try to find the most optimum solution. It is important to note here that expecting a perfect solution is not practical, especially as the problem grows larger. In the case of dance choreography, this is about when the amalgation length, the number of different figures, exceeds 10.
### Exhaustive Algorithms
In an exhaustive algorithm, every eventuality is investigated and it backtracks as it searches. Though this does eventually find the most optimum solution, it is not very efficient and will take exponential time in the worst case scenario.

## Real World Applications

## Evaluation
The way that the author defined dance, as a series of figures that could or could not be connected in different ways was very clever. It allowed it to take a form distinctly related to graphs, which made the proof process much easier.

However, dance is an art not a science and it follows from that that an optimized order of figures probably won’t automatically make the best dance routine.

## For more information

Read his article, [here](http://dl6.globalstf.org/index.php/joc/article/download/1092/1025/).
