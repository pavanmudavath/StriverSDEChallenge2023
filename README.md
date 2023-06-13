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

