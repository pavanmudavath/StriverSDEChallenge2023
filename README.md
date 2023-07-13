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
    
    
    
    
    //linked list
    //singleLinkedList
   

public class Main
{
    private Node head;
    private Node tail;
    
    private int size;
    public Main(){
        this.size=0;
    }
    public void insertFrist(int val){
        Node node=new Node(val);
        node.next=head;
        head=node;
        if(tail==null){
            tail=head;
        }
        size+=1;
    }
    public void insertLast(int value){
        Node node=new Node(value);
         if(tail==null){
            insertFrist(value);
            return;
        }
        tail.next=node;
        tail=node;
        size++;
        
    }
    public void insert(int value,int index){
        if(index==0){
            insertFrist(value);
            return;
        }
        if(index==size){
            insertLast(value);
            return;
        }
        Node temp=head;
        for(int i=1;i<index;i++){
            temp=temp.next;
        }
        Node node=new Node(value,temp.next);
        temp.next=node;
        size++;
    }
    
    public int deleteFrist(){
        if(head==null){
            head=tail;
        }
        int val=head.value;
        head=head.next;
        size--;
        return val;
    }
    public int  deleteLast(){
      if(size<=1){
          return deleteFrist();
      }
      Node secondLast=get((size) - 2);
      int val=tail.value;
      tail=secondLast;
      tail.next=null;
      return val;
    }
    public Node get(int index){
        Node node=head;
        for(int i=1;i<index;i++){
            node=node.next;
        }
        return node;
    }
    
    public int delete(int index){
        if(index==0){
            return deleteFrist();
        }
        if(index==size-1){
            return deleteLast();
        }
        Node prev=get(index-1);
        int val=prev.next.value;
        prev.next=prev.next.next;
        
        return val;
    }
    public int find(int value){
        Node node=head;
        while(node!=null){
            if(node.value==value){
                return node.value;
            }
            node=node.next;
        }
        return -1;
    }
    public void display(){
       Node temp=head;
        while(temp!=null){
            System.out.print(temp.value+"->");
            temp=temp.next;
        }
        System.out.print("Null");
    }
    private class Node{
        private int value;
        private Node next;
    
    
   public Node(int value){
        this.value=value;
    }
    
  public Node(int value,Node next){
        this.value=value;
        this.next=next;
    }
}
    
    
	public static void main(String[] args) {
	Main main=new Main();
	main.insertFrist(3);
	main.insertFrist(4);
	main.insertFrist(5);
	main.insertFrist(6);
	main.insertLast(17);
	main.display();
	System.out.println();
	main.deleteFrist();
	main.display();
	System.out.println();
System.out.print(main.deleteFrist());	
	
	}
}























//SUDOKU
public class Main{
    public static void main(String args[]){
        int board[][]=new int[][]{
    {5, 3, 0, 0, 7, 0, 0, 0, 0},
    {6, 0, 0, 1, 9, 5, 0, 0, 0},
    {0, 9, 8, 0, 0, 0, 0, 6, 0},
    {8, 0, 0, 0, 6, 0, 0, 0, 3},
    {4, 0, 0, 8, 0, 3, 0, 0, 1},
    {7, 0, 0, 0, 2, 0, 0, 0, 6},
    {0, 6, 0, 0, 0, 0, 2, 8, 0},
    {0, 0, 0, 4, 1, 9, 0, 0, 5},
    {0, 0, 0, 0, 8, 0, 0, 7, 9}
    };

       if(solve(board)){
        display(board);
        }
    else{
       System.out.println("cannot solve");
         }
    }
public static boolean solve(int[][] board){
        int n=board.length;
        int row=-1;
        int col=-1;
        
        boolean emptyLeft=true;
        
        //this is how we are replacing the r,c from arguments
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                if(board[i][j]==0){
                    row=i;
                    col=j;
                emptyLeft=false;
                break;
                }
            }
            
            //if you find any empty element in row ,then break It
            if(emptyLeft==false){
                break;
            }
        }
        if(emptyLeft==true){
            return true;
            //suduko is solverd
        }
        
        //backTrack
        for(int number=1;number<=9;number++){
            if(isSafe(board,row,col,number)){
                board[row][col]=number;
                if(solve(board)){
                    //found the ans 
                    //display(board);
                    return true;
                }
                else{
                    //backTrack
                    board[row][col]=0;
                }
            }
        }
        return false;
        
    }
    public static void display(int[][] board){
        for(int[] row:board){
            for(int num:row){
                System.out.print(num+" ");
            }
            System.out.println();
        }
    }
    
    public static boolean isSafe(int board[][],int row,int col,int num){
        //check if the row
        for(int i=0;i<board.length;i++){
            //check if is the number in the row
            if(board[row][i]==num){
                return false;
            }
        }
        
         //check if the col
        for(int nums[]:board){
            //check if is the number in the col
            if(nums[col]==num){
                return false;
            }
        }
        
        
        // for sqrt matrix
        int sqrt=(int)(Math.sqrt(board.length));
        int rowStart=row-row%sqrt;
        int colStart=col-col%sqrt;
        
        for(int r=rowStart;r<rowStart+sqrt;r++){
            for(int c=colStart;c<colStart+sqrt;c++){
                if(board[r][c]==num){
                    return false;
                }
            }
        }
        return true;
        
        
    }
}

























/*

// NKnights problem

public class Main{
    public static void main(String args[]){
        int n=4;
        boolean[][] board=new boolean[n][n];
        NKnights(board,0,0,4);
    }
    public static void NKnights(boolean board[][],int row,int col,int knights){
        if(knights==0){
            display(board);
            System.out.println();
            return;
        }
        if(row==board.length-1 && col==board.length){
            return;
        }
        
        if(col==board.length){
            NKnights(board,row+1,0,knights);
            return;
        }
        if(isSafe(board,row,col)){
            board[row][col]=true;
            NKnights(board,row,col+1,knights-1);
            board[row][col]=false;
        }
        NKnights(board,row,col+1,knights);
    }
    
    private static boolean isSafe(boolean board[][],int row ,int col){
        if(isValid(board,row-2,col-1)){
            if(board[row-2][col-1]){
                return false;
            }
        }
        
        if(isValid(board,row-1,col-2)){
            if(board[row-1][col-2]){
                return false;
            }
        }
        
        if(isValid(board,row-2,col+1)){
            if(board[row-2][col+1]){
                return false;
            }
        }
        
        if(isValid(board,row-1,col+2)){
            if(board[row-1][col+2]){
                return false;
            }
        }
        return true;
        
    }
    // do not repeate your self hence this function created.
    static boolean isValid(boolean board[][],int row ,int col){
        if(row>=0 && row<board.length && col>=0 && col<board.length){
            return true;
        }
        return false;
    }
    
    
    private static void display(boolean board[][]){
	    for(boolean[] row:board){
	        for(boolean element: row){
	            if(element){
	                System.out.print("K ");
	            }
	            else{
	                System.out.print("X ");
	            }
	            
	        }
	        System.out.println();
	    }
	}
}








public class Main
{
	public static void main(String[] args) {
		int n=4;
		boolean board[][]=new boolean[n][n];
		System.out.println(queens(board,0));
	}
	public static int queens(boolean board[][],int row){
	    if(row==board.length){
	        display(board);
	        System.out.println();
	        return 1;
	    }
	    int count=0;
	    //placing the queen and checking the every col and row
	    for(int col=0;col<board.length;col++){
	        //place if the queue is safe
	        if(isSafe(board,row,col)){
	            board[row][col]=true;
	            count+=queens(board,row+1);
	            board[row][col]=false;
	        }
	    }
	    return count;
	}
	
	private static boolean isSafe(boolean board[][],int row,int col){
	    //check vertical row 
	    for(int i=0;i<row;i++){
	        if(board[i][col]){
	            return false;
	        }
	    }
	    //diagonal left
	    int maxLeft=Math.min(row,col);
	    for(int i=1;i<=maxLeft;i++){
	        if(board[row-i][col-i]){
	            return false;
	        }
	    }
	    //diagonal right
	    int maxRight=Math.min(row,board.length-col-1);
	        for(int i=1;i<=maxRight;i++){
	            if(board[row-i][col+i]){
	                return false;
	            }
	        }
	 return true;       
	}
	
	
	private static void display(boolean board[][]){
	    for(boolean[] row:board){
	        for(boolean element: row){
	            if(element){
	                System.out.print("Q ");
	            }
	            else{
	                System.out.print("X ");
	            }
	            
	        }
	        System.out.println();
	    }
	}
}
*/
