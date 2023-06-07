# StriverSDEChallenge2023
class Solution {
    public void setZeroes(int[][] matrix) {
       int row=matrix.length;
       int col=matrix[0].length;
       Set<Integer>zeroRow=new HashSet<>();
       Set<Integer>zeroCol=new HashSet<>();

       //find the seros in the matrix
       for(int i=0;i<row;i++){
           for(int j=0;j<col;j++){
               if(matrix[i][j]==0){
                   zeroRow.add(i);
                   zeroCol.add(j);
               }
           }
       }
       //make the rows and clnm zero
       for(int i=0;i<row;i++){
           for(int j=0;j<col;j++){
               if(zeroRow.contains(i) || zeroCol.contains(j)){
                   matrix[i][j]=0;
               }
           }
       }
