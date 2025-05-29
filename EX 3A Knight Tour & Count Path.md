# EX 3A Knight Tour & Count Path
## DATE:11.03.2025
## AIM:
To write a python program to find minimum steps to reach to specific cell in minimum moves by knight

## Algorithm
1. Use Breadth-First Search (BFS) starting from the knight’s position.
2. Enqueue the starting position with distance 0 and mark it as visited.
3. At each step, dequeue a cell and check if it is the target position.
4. If not, move the knight in all 8 possible moves and enqueue valid, unvisited cells with dist + 1.
5. Repeat until the target is reached, and return the number of steps (distance).
   
## Program:
```

Program to implement to find minimum steps to reach to specific cell in minimum moves by knight.
Developed by: SHABREENA VINCENT
Register Number:212222230141
```
```
import sys
class KnightsTour:
    def __init__(self, width, height):
        self.w = width
        self.h = height
        self.board = []
        self.generate_board()

    def generate_board(self):
        for i in range(self.h):
            self.board.append([0]*self.w)

    def print_board(self):
        
        for elem in self.board:
            print (elem)
       
    def generate_legal_moves(self, cur_pos):
        possible_pos = []
        move_offsets = [(1, 2), (1, -2), (-1, 2), (-1, -2),
                        (2, 1), (2, -1), (-2, 1), (-2, -1)]
        ############### Add your code here ##############################
        for offset in move_offsets:
            new_x=cur_pos[0]+offset[0]
            new_y=cur_pos[1]+offset[1]
            if 0<=new_x<self.h and 0 <=new_y<self.w and self.board[new_x][new_y]==0:
                possible_pos.append((new_x,new_y))

        return possible_pos

    def sort_lonely_neighbors(self, to_visit):
        neighbor_list = self.generate_legal_moves(to_visit)
        empty_neighbours = []

        for neighbor in neighbor_list:
            np_value = self.board[neighbor[0]][neighbor[1]]
            if np_value == 0:
                empty_neighbours.append(neighbor)

        scores = []
        for empty in empty_neighbours:
            score = [empty, 0]
            moves = self.generate_legal_moves(empty)
            for m in moves:
                if self.board[m[0]][m[1]] == 0:
                    score[1] += 1
            scores.append(score)

        scores_sort = sorted(scores, key = lambda s: s[1])
        sorted_neighbours = [s[0] for s in scores_sort]
        return sorted_neighbours

    def tour(self, n, path, to_visit):
        self.board[to_visit[0]][to_visit[1]] = n
        path.append(to_visit) #append the newest vertex to the current point
        if n == self.w * self.h: #if every grid is filled
            self.print_board()
            print (path)
            print ("Done!")
            sys.exit(1)

        else:
            sorted_neighbours = self.sort_lonely_neighbors(to_visit)
            for neighbor in sorted_neighbours:
                self.tour(n+1, path, neighbor)
                self.board[to_visit[0]][to_visit[1]] = 0
            try:
                path.pop()
            except IndexError:
                print ("No path found")
                sys.exit(1)

if __name__ == '__main__':
    x=int(input())
    y=int(input())
    kt = KnightsTour(x,y)
    kt.tour(1, [], (0,0))
    kt.print_board()
```
## Output:
![image](https://github.com/user-attachments/assets/30c309c9-ec19-4c96-8072-992ee7a945e4)

## Result:
The program executed successfully, and the minimum number of steps for the knight to reach the target was calculated.
