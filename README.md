# Sudoku-Solver

This is my solution to the problem of making an algorithm solve a Sudoku board.
The solution includes a back-tracking approach to solve this problem.

Backtracking:
-------------
  Backtracking is an recursive way of solving problems where the solution is built in small increaments, one increament at a time. Instead of trying all the possible values, this approach, when fails backtracks to the last successful step and changes the value of the next step to further the solution.
  
Another solution to this problem can be an iterative model where all the possible numbers are tried at all the empty positions.
However, this approach takes a lot of time and is not the most ideal way to find the correct solution.

Step-by-Step Solution:
----------------------
1. Finding empty spaces on the board:
    While on a console, the empty spaces on a board can be identified as '0'. A function to find such empty spaces can easily be          
    written.
    
    def findEmpty(bo):
    for i in range(len(bo)):
        for j in range(len(bo[0])):
            if bo[i][j]==0:
                return (i,j)
    return None
    
2. Validating the position once the value is placed:
    We can fill in any values, but to find the correct value for the position, we have to validate 3 important rules of Sudoku.
    
    a) Filled number should not be present in the same row (Easy)
        
        #Check Row
        for i in range(len(bo[0])):
          if bo[pos[0]][i]==num and pos[1]!=i:
              return False
              
    b) Filled number should not be present in the same column (Also Easy)
    
         #Check Column
         for i in range(len(bo)):
            if bo[i][pos[1]]==num and pos[0]!=i:
              return False

    c) Filled number should not be present in the same box (Realatively difficult)
    
        #Check Box
        box_x=pos[1]//3   #To determine the 3/3 box
        box_y=pos[0]//3   #To determine the 3/3 box
        for i in range(box_y*3, box_y*3+3):
          for j in range(box_x*3, box_x*3+3):
            if bo[i][j]==num and (i,j)!=pos:
                return False
                
     In the end, if all the above conditions are true, the number filled for the postion is true.(For now)

3. To recursively solve the board, we can call the above functions in our solve function, which will call iteself recursively
   until a correct solution for all the positions in the board is found.
   
   def solve(bo):
    find=findEmpty(bo)
    if not find:
        return True
    else:
        row,col=find
    for i in range(1,10):
        if validatePos(bo,i,(row,col)):
            bo[row][col]=i
            if solve(bo):
                return True
            bo[row][col]=0    #backtracking
    return False
    
4.  The final step to our solution is to show the board with the correct solution.
    
    def showBoard(bo):
    for i in range(len(bo)):
        if i%3==0 and i!=0:
            print('- - - - - - - - - - - - ')
        for j in range(len(bo[0])):
            if j%3==0 and j!=0:
                print(' | ',end="")
            if j==8:
                print(bo[i][j])
            else:
                print(str(bo[i][j])+' ',end='')


The above functions can be called to solve any given sudoku board as there are no dynamic values used for the size of the board.
Go on !! Try it ;p
