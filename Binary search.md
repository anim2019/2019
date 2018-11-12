1. Recursion:

1.1 Fibonacci
recursion:
** Time = O(2^n) There are n levels in the recursions tree. At most there are 2^n nodes in the tree. So the time complexity is 2^n
** Space = O(n) Since there're n levels and each level it contains 1 local variable.

Non-recursion:
public int fibonacci(int n) {
    int a = 0, b = 1;
     for (int i = 0; i < n - 1; i++) {
         int c = a + b;
         a = b;
         b = c;
     }

    return a;
}

1.2 a^b
recursion:
int getAPowB(int a, int b) {
  if (b == 0) {
    return 1;
  }
  
  int halfResult = getAPowB(a, b/2);
  if (b % 2 == 0){
    return halfResult * halfResult;
  } else {
    return halfResult * halfResult * a;
  }
}

