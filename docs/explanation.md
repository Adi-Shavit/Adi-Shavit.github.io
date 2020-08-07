# Exact Cover Problem
The `Exact Cover` problem is a staple in computer science. It is a question that states:
_"Given a collection S of subsets of set X, an exact cover is the subset S* of S such that each element of X is contained is **exactly one** subset of S*"_

> This problem also has a practical aspect to it as many problems in computer science can described as exact cover problems. (the problem of tiling a board with pentominoes, and solving Sudoku can both be viewed as exact cover problems)

Given the following matrix S:
|     |A|B|C|D|E|F|G|
|-----|-|-|-|-|-|-|-|
|**1**|1|0|0|1|0|0|1|
|**2**|1|0|0|1|0|0|0|
|**3**|0|0|0|1|1|0|1|
|**4**|0|0|1|0|1|1|0|
|**5**|0|1|1|0|0|1|1|
|**6**|0|1|0|0|0|0|1|

Given the following matrix the subset S* would be:
|     |A|B|C|D|E|F|G|
|-----|-|-|-|-|-|-|-|
|**2**|1|0|0|1|0|0|0|
|**4**|0|0|1|0|1|1|0|
|**6**|0|1|0|0|0|0|1|

In the subset S* you can see that the values of rows 2, 4, 6 cover the subset X exactly.


# Algorithm X
Algorithm x is a proposed solution to the exact cover problem by Donald Knuth. 
In his original paper Knuth showed that the exact cover problem can be efficiently solved using **Dancing Links** (A more detailed explanation will arrive later)
For now remember that this technique was coined by **Donald Knuth** as `DLX`.

Algorithm X is a recursive, depth-first, backtracking algorithm. It is non-deterministic in nature, so for the same input, it can exhibit different behaviors.

## Pseudocode
The pseudo code for Algorithm X is:
 1. If the matrix A has no columns, the current partial solution
    is a valid solution -> terminate successfully.
 2. Otherwise, choose a column c (deterministically).
 3. Choose a row r such that A[r] = 1 (nondeterministically).
 4. Include row r in the partial solution.
 5. For each column j such that A[r][j] = 1,
        for each row i such that A[i][j] = 1,
            delete row i from matrix A.
      delete column j from matrix A.
 6. Repeat this algorithm recursively on the reduced matrix A.

# Real world problems
Many problems in the real world can be reduced to exact cover. For the case of this write-up we'll look at two main examples: `Solving sudoku` and `Tiling Pentominos`. For each of these examples we'll examine them first with a simplistic view of `Algorithm X` and then with the addition of Dancing links in order to improve the algorithm.

## Sudoku
Describing Sudoku as an exact cover problem is actually more intuative than you might think.
Just in case Sudoku isn't a game you're familiar with, the rules of the game are as follows:
`In classic sudoku, the objective is to fill a 9×9 grid with digits so that each column, each row, and each of the nine 3×3 subgrids that compose the grid (also called "boxes", "blocks", or "regions") contain all of the digits from 1 to 9. The puzzle setter provides a partially completed grid, which for a well-posed puzzle has a single solution.`

### Conversion to exact cover problem
In order to convert `Sudoku` to an exact cover problem all you have to do is find the constraints. `Sudoku` has the following constraints:
 1. **Row-Column:** Each intersection of a row and column, i.e, each cell, must contain exactly one number. (9*9=81 total constraints)
 2. **Row-Number:** Each row must contain each number exactly once. (9*9=81 total constraints)
 3. **Column-Number:** Each column must contain each number exactly once. (9*9=81 constraints)
 4. **Box-Number:** Each box must contain each number exactly once. (9*9=81 total constraints)

These constraints are simple but crucial nevertheless in order to define the parameters of the game.
### Building the matrix
In order to build the matrix lets examine a regular 9X9 sudoku board.


| 5 | 3 |   |   | 7 |   |   |   |   |
|---|---|---|---|---|---|---|---|---|
| 6 |   |   | 1 | 9 | 5 |   |   |   |
|   | 9 | 8 |   |   |   |   | 6 |   |
| 8 |   |   |   | 6 |   |   |   | 3 |
| 4 |   |   | 8 |   | 3 |   |   | 1 |
| 7 |   |   |   | 2 |   |   |   | 6 |
|   | 6 |   |   |   |   | 2 | 8 |   |
|   |   |   | 4 | 1 | 9 |   |   | 5 |
|   |   |   |   | 8 |   |   | 7 | 9 |

Because we can assign 9 numbers for each cell and the board is 9X9 we know that there are `9*9*9=729` possibilities. We also know that there are a total of `4*81=324` possible constraints. 
Thus this problem can be represented by a 729×324 matrix (Because we receive some clues some of our options are removed and chosen for us).
> **Terminology:** R1 = Row 1, C1 = Column 1, #1 = value 1 => `R1C1#5` = value at `(1,1) = 5`

**What will be our columns?**
> Each column represents a number being placed in any of the 9×9 positions, then each of the possible numbers per rows, column, and group. This brings us to 9×9+9×9+9×9+9×9=324 columns of the matrix.

**What will be our rows?**
> They are simply a 1 in each of the columns that specify a) which position of the board the number is in, b) what column and number are used, c) what row and number are used, and d) what group and number are used.

The exact cover in this case is: "select all rows of a matrix where there is a single 1 per column."



# Dancing Links
Dancing links are an idea popularized by `Donald Knuth` back in 1979. Dancing links is a technique for _reverting_ the operation of deleting a node from a _circular doubly linked list_


