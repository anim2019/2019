### kth smallest number in sorted matrix
记住iterate k-1次循环，因为第一个已经加到了priority queue 里面

```java

public class Solution {
  public int kthSmallest(int[][] matrix, int k) {
    // Write your solution here.
    if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
      return 0; 
    }
    PriorityQueue<Point> queue = new PriorityQueue<Point>(k, new Comparator<Point>() {
      @Override
      public int compare(Point p1, Point p2) {
        if (p1.val == p2.val) {
          return 0;
        }
        return p1.val < p2.val ? -1 : 1;
      }
    });
    
    boolean[][] visited = new boolean[matrix.length][matrix[0].length];
    
    queue.offer(new Point(0, 0, matrix[0][0]));
     visited[0][0] = true;
    
    int row = matrix.length, col = matrix[0].length;
    // iterate k times to find k smallest number
    for (int i = 0; i < k - 1; i++) {
      Point point = queue.poll();
     
      if (point.x + 1 < row && !visited[point.x + 1][point.y]) {
        queue.offer(new Point(point.x + 1, point.y, matrix[point.x + 1][point.y]));
        visited[point.x + 1][point.y] = true;
      }
      
      if (point.y + 1 < col && !visited[point.x][point.y + 1]) {
        queue.offer(new Point(point.x, point.y + 1, matrix[point.x][point.y + 1]));
        visited[point.x][point.y + 1] = true;
      }
      
    }
    
    return queue.peek().val;
  }
}

class Point {
  int x;
  int y;
  int val;
  public Point(int x, int y, int val) {
    this.x = x;
    this.y = y;
    this.val = val;
  }
}

```

### check if binary tree is completed
每一次只考虑下一层，如果左孩子是空，那么flag = true，则右孩子必须为空，否则返回false；如果右孩子是空，那么flag = true，则右孩子下一层的孩子必须为空。

```java

/**
 * public class TreeNode {
 *   public int key;
 *   public TreeNode left;
 *   public TreeNode right;
 *   public TreeNode(int key) {
 *     this.key = key;
 *   }
 * }
 */
public class Solution {
  public boolean isCompleted(TreeNode root) {
    // Write your solution here
    if (root == null) {
      return true; 
    }
    
    Queue<TreeNode> queue = new LinkedList<TreeNode>();
    queue.offer(root);
    // if the flag == true, then there should not be any node afterwards
    boolean flag = false;
    
    while (!queue.isEmpty()) {
      TreeNode node = queue.poll();
      //check left node
      if (node.left == null){
        // if left node is null, then there should not be any node afterwards
        flag = true;
      } else if (flag) {
        return false; 
      } else {
        queue.offer(node.left); 
      }

      //check right node
      if (node.right == null) {
        // if right node is null, then there should not be nodes as children of next level nodes
        // since only when we check if (next level) node.left == null, it will trigger return  
        flag = true; 
      } else if (flag) {
        return false; 
      } else {
        queue.offer(node.right); 
      }
    }
    return true;
  }
}


```


