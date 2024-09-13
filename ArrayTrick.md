int xy plane if you have to move left, right direction at any point you can use dir array
                N      E     S        w
int[][]  dir = {{0,1},{1,0},{0, -1},{-1,0}}; // rember keep the direction in order i.e, N E S W or E S W N  both are fine you can have any start direction it will work.
 
 suppose your initial direction is north i.e, idx = 0;

 for right direction from any position your index will be   idx = (idx+1)%4;  N  r-->  E l--> N  so +1 is right direction index of dir and -1 is left direction index of dir (idx + 3)%4 is equivalent to -1 idx of any position

 for left direction from any position you index will be   idx = (idx+3)%4;



 # ---------------------------------------------------------------
 sorted 2d matrix
 to to binary search  take  => s=0,  end = row*col -1;  int mid = (s+e)/2;
 to get element  of mid do this =>  matrix[mid/col][mid%col]

 eg: 4 X 6 matrix given => end = 4*6-1=23;

 to get 23rd elt  r => 23/6 = 3; c => 23%6=5;  matrix[3][5] = 23rd element of matrix.
 