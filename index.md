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
In his article “The Complexity of Dance Choreography Procedures”, Nigel Gwee seeks to define the complexity of dance choreography. Gwee narrowly defines the dances he’s computationally choreographing as a finite number of figures, positions or motions that a dancer might perform. Additionally, he defines a number of tuples defining possible interactions between these figures so that a choreography won’t demand a dancer to move in a way that is not possible. 

Having defined his parameters, Gwee sets out to prove that choreographing a dance is a NP-complexity problem. Through proving this, he would show that the problem of dance choreography is easily transformable into many others. This opens the door to using already existing algorithms to find solutions to posed choreography problems.

## Background Information
**Complexity Theory:**
Complexity theory seeks to answer a few problems, one overarching and one problem-specific. The first is whether the category of problems that can be solved in polynomial time the same as the category of problems which can be verified in polynomial time through a non-deterministic method that generates possible solutions. In other words, P=NP?

The second, problem specific one is which complexity category does the problem belong in. In the case of this paper, that means determining which categories these choreography problems belong in and how they can be linked to help solve each other.

**NP Complexity Classes:**
Non-determinism is useful because it allows us to suspend some concerns, such as an actual solution -- for NP, we only have to prove that you can verify a given solution in polynomial time, we don’t actually need to find a solution. The goal of this paper is, therefore, not to find particular solutions but to classify the process through which they might be found. THe categories, which we did cover in class, are defined as the following:

- NP-Complete as a subcategory of NP-Complex, composed of problems where an efficient solution to one would lead to such a solution to all of them -- they are all at least as difficult as each other.
  -  binary responses of yes/no
- Also within NP-Complexity are NP-Hard, NP-Easy, and NP-Equivalent classes
  -  NP-Hard problems are often optimization problems related to NP-Complete problems, but with answers more complex than a binary yes/no
  -  These are often at least as difficult again as NP-Complete problems but no more difficult than any other NP problem (NP-Easy)
  -  If a problem is both NP-Hard and NP-Easy, it’s NP-Equivalent
- “This implies that the decision problem and the related optimization problem that have been categorized as NP-Complete, and NP-Hard/Easy, respectively, are “equivalent” from the efficiency aspect.” 

## Decision Problems
These decision problems are constructed with the aim of determining not a particular choreography but whether, given a set of figures and ways they can be combined and a few other restrictions, a choreography can or cannot be assembled. These problems serve as the base for the following optimization problems, which allow for more specifications.

### Dance Choreography (DC)
Dance Choreography is the base problem for this proof that all following problems rely on. It is composed of the Instance, which specifies the components of the problem, and the Question, which specifies what the problem is.

**Instance**
- A finite set of _Figures_;
- a set _Follow_ of tuples <f-i, f-j>, f-i, f-j in _Figures_;
- n in Natural Numbers;
- _f-start_, _f-end_ in _Figures_;
- a set _Compulsory_ that is a subset of _Figures_

**Question**
- Is there a sequence _Amalgamation_ = <f-1, f-2, …, f-n>,
  -  f-i in _Figures_, 1<=i<=n, and <f-j, f-j+1> in _Follow_, 1<=j<=n
- Such that 
  -  f-1 = _f-start_ and f-n = _f-end_
- And
  -  {f-i: 1<=i<=n} is a subset of _Compulsory_?
  
To show DC to be NP-Complete, you must show that a solution (found non-deterministically) is verifiable in polynomial time. In order to verify a solution to DC, you must simply confirm that figures used in _Amalgamation_ are valid with regards to _Follow_, contained in _Compulsory_, and begin and end with the designated figures, _f-start_ and _f-end_.

The second part of proving DC is NP-Complete requires another NP-Complete problem that has already been proven to fit into the category. From there, if DC can be transformed into it in polynomial time then DC must also be NP-Complete. This brings us to the next problem:

### Hamiltonian Circuits (HC)
A Hamiltonian Circuit (HC) is a known NP-Complete problem on a graph which asks whether the graph includes a simple circuit containing all vertices. 

![Image](https://www3.cs.stonybrook.edu/~skiena/combinatorica/animations/anim/ham.gif)

_src: https://www3.cs.stonybrook.edu/~skiena/combinatorica/animations/anim/ham.gif_

DC can be given certain parameters to create a HC:
- Set _Compulsory_ equal to _Figures_ so that the two sets contain all of the “vertices” 
- Set _f-start_ = _f-end_ so that DC ends where it starts and creates a circuit to fulfill the requirements of a HC

Since by restricting DC with these requirements we can convert it to a HC, it must also be NP-Complete.

### Dance Choreography k (DCk)
In order to transition from a decision problem to an optimization problem, we must introduce the concept of distinctness by introducing a variable k to the Instance. k must be contained in the set of natural numbers, including 0. To the question, we include the added restriction that the number of distinct elements f-1 through f-n must be greater than or equal to the value of k. 

The problem does not change substantially to the point where it isn’t clearly restrictable to DC. Do this and set k to 0. Since DCk is transformable to DC and DC can be transformed into a Hamiltonian Circuit, which is NP-Complete, DCk is also NP-Complete.


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
### Heuristic Algorithms: The Greedy Algorithm
Heuristic algorithms are algorithms in which a practical approach is applied to reach a possible solution. The most optimal solution may not be the result, but a "good enough" solution is. 

The Greedy Algorithm is an example of a heuristic algorithm in which at each step the "best choice" is made and there is no backtracking. This algorithm is much faster than its counterpart, the exhaustive algorithm, however, the optimal solution is not guarenteed.

![Image](https://ds055uzetaobb.cloudfront.net/brioche/uploads/EKKlGLuUQd-greedy-search-path.gif?width=300)

## Real World Applications

## Evaluation
The way that the author defined dance, as a series of figures that could or could not be connected in different ways was very clever. It allowed it to take a form distinctly related to graphs, which made the proof process much easier.

However, dance is an art not a science and it follows from that that an optimized order of figures probably won’t automatically make the best dance routine.

## For more information

Read his article, [here](http://dl6.globalstf.org/index.php/joc/article/download/1092/1025/).
