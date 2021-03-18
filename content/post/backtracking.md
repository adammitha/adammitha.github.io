+++
author = "Adam Mitha"
title = "Tackling Backtracking Search"
date = "2021-03-11"
description = "Approach to solving backtracking search problems in Go."
tags = [
    "Go",
]
categories = [
    "tutorials",
]
series = [
  "Tutorials",
]
+++

## Introduction
Anyone's who's taken CPSC 110 at UBC probably experiences a sense of dread when they hear about search problems. This is not an unreasonable response — backtracking search problems are among the hardest that you'll encounter on interview practice sites like [Leetcode](http://www.leetcode.com), so it seems almost cruel to expect first year computer science students (many of whom have never programmed in their life) to be able to tackle them. However, like with any other problem that you'll encounter in 110 (or in software engineering generally), having a structured approach to backtracking can help turn a seemingly gargantuan task into one that's quite digestible. There's only one way to eat an elephant — one bite at a time.

### Premise

The premise of backtracking search problems is that we are generating an n-ary (or arbitrary-arity) tree of potential solutions to our problem, and then searching through that generated tree to find our solution. As a quick reminder, an n-ary tree is a tree where each node can have an arbitrary number of children. This differs from a binary search tree, where each node has exactly two children. 

### Illustrative exampe: N-Queens

I'll be using the [N-Queens](https://developers.google.com/optimization/cp/queens) problem to demonstrate my approach to backtracking search problems:
> How can N queens be placed on an NxN chessboard so that no two of them attack each other?
>

For example, 4 queens can be placed on a 4x4 chess board like this:

{{< figure src="/images/sol_4x4_b.png" >}}

While this may seem intimidating at first, as you'll see a structured approach will make this problem much easier.

### Tools

I'll be using [Go](https://golang.org/) to develop my solution to this problem, but I won't be using any third-party packages so you should be able to reproduce my solution in your language of choice.

## Step 1: Modelling the search state
The first step in any backtracking search problem is to determine what we are searching for, and how to best represent that in a data structure. In other words, what will represent the 'node' in the n-ary tree of solutions we are searching through.

In the context of the N-queens problem, we are looking for a chess board that contains N-queens that cannot attack each other. In short, we are searching for a chess board, so that's what we'll model as our search state. A chess board is essentially a grid, which can be represented using a 2-dimensional array. We also need a way to represent which squares in the board are occupied. This can be done using a boolean value — `true` means a queen is in that square, and `false` means it's empty.

A simple function can be used to generate an empty board of size N x N.

```go
// Board is a two-dimensional array of boolean values representing a chess board
type Board [][]bool

// NewBoard creates an empty Board of size n x n
func NewBoard(n int) *Board {
  board := make(Board, n)
  
  for i := 0; i < n; i++ {
    board[i] = make([]int, n)
    for j := 0; j < n; j++ {
      board[i][j] = false
    }
  }
  
  return &board
}
```



## Step 2: Generating child nodes





## Step 3: Scaffolding the search function

Now that we've established the 'node' for the tree we are searching, we can start laying out the scaffolding for a function that will search through the tree for our solution. 

At a high level, this function consumes a board and will do the following:

1. Check the board to see if it's solved. If it is, return it. If not, proceed to step 2.
2. 

```go
func search(board *Board) *Board, err {
  if board.solved() {
    return board
  }
  
  nextBoards := board.nextBoards()
  
  for board := range nextBoards {
    solution, err := search(board)
    if err != nil {
      continue
    }
    
    return solution
  }
  
  return nil, fmt.Errorf("Unable to find a solution!")
}
```

