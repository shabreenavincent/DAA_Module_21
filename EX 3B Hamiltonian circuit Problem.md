# EX 3B Hamiltonian Circuit Problem
## DATE:15.03.2025
## AIM:
To write a python program to check whether Hamiltonian path exits in the given graph.

## Algorithm
1. Start from each vertex and mark it as visited.
2. Try visiting all other vertices one by one using edges.
3. Use dynamic programming to remember visited sets and paths.
4. If you can visit all vertices exactly once, a Hamiltonian path exists.
5. If no such path is found after checking all options, return "NO".
## Program:
```

Program to implement to check whether Hamiltonian path exits in the given graph.
Developed by:SHABREENA VINCENT
Register Number:212222230141
```
```
class Graph():
    def __init__(self, vertices):
        self.graph = [[0 for column in range(vertices)]
                            for row in range(vertices)]
        self.V = vertices
    def isSafe(self, v, pos, path):
        if self.graph[ path[pos-1] ][v] == 0:
            return False
        for vertex in path:
            if vertex == v:
                return False
 
        return True
    def hamCycleUtil(self, path, pos):
        ######################Add your code here#################################
        #Start here
        if pos == self.V:
            if self.graph[ path[pos-1] ][ path[0] ] == 1:
                return True
            else:
                return False
        for v in range(1,self.V):
            if self.isSafe(v, pos, path) == True:
                path[pos] = v
                if self.hamCycleUtil(path, pos+1) == True:
                    return True
                path[pos] = -1
        return False
        #End here
 
    def hamCycle(self):
        path = [-1] * self.V
        path[0] = 0
 
        if self.hamCycleUtil(path,1) == False:
            print ("Solution does not exist\n")
            return False
 
        self.printSolution(path)
        return True
 
    def printSolution(self, path):
        print ("Solution Exists: Following",
                 "is one Hamiltonian Cycle")
        for vertex in path:
            print (vertex, end = " ")
        print (path[0], "\n")
g1 = Graph(5)
g1.graph = [ [0, 1, 0, 1, 0], [1, 0, 1, 1, 1],
            [0, 1, 0, 0, 1,],[1, 1, 0, 0, 1],
            [0, 1, 1, 1, 0], ]
g1.hamCycle();
```
## Output:
![image](https://github.com/user-attachments/assets/95dd6474-3f27-4a5d-a292-0106d34c38eb)

## Result:
The Hamiltonian path program executed successfully, and it determined whether a Hamiltonian path exists in the given graph.
