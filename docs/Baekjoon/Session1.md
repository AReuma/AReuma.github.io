---
layout: default
title: 2490번 :윷놀이
parent: Baekjoon
---

# [백준] 2490번 - 윷놀이 [JAVA]
  
[2490번: 윷놀이](https://www.acmicpc.net/problem/2490)  
  
  
![2490번: 윷놀이](/assets/images/Baekjoon/Session1/img.png)
    
*** 
    
### 1. 문제 풀이
    
```java
public class Main {
    public String solution(int[] arr){
        int z = 0;

        for(int i = 0; i < 4; i++){
            if(arr[i] == 0) z++;
        }

        return switch (z) {
            case 1 -> "A";
            case 2 -> "B";
            case 3 -> "C";
            case 4 -> "D";
            default -> "E";
        };
    }

    public static void main(String[] args) throws IOException {
        Main T = new Main();
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        int[][] arr = new int[3][4];

        for(int i = 0; i < 3; i++){
            String s = br.readLine();
            StringTokenizer st = new StringTokenizer(s);

            for(int j = 0; j < 4; j++){
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        for (int[] a : arr) {
            bw.write(T.solution(a)+"\n");
        }
        bw.close();
    }
}
```    
    
쉽게 0의 개수를 세서 나누는 방식으로 풀었다.  
크게 생각하지 않고 for문을 통해서 받고 받은 배열을 통해 개수를 세면 된다고 생각했으나  
for문을 여러번 돌아야하는가에 대한 고민이 발생함.  
    
입력받을때 이중 for문을 돌고  
solution 메서드를 부를때 for문을 돌고  
0의 개수를 셀때 또 for문을 돌아서 총 4번을 돌게 된다.  
    
  
그래서 처음부터 0의 개수나 1의 개수를 받으면 어떻게될까 고민을함.  
    
1의 개수를 받으면 1의 개수를 세는거나, 받은 배열의 값 모두를 더하는거랑 값이 동일함.  
그래서 다른 방법으로 시도해봄.  
    
    
***    
       
    
### 2. 문제풀이 
    
```java
public class Main {
    public static void main(String[] args) throws IOException {
        String[] arr =  {"D", "C", "B", "A", "E"};

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        StringBuilder sb = new StringBuilder();

        for(int i = 0; i < 3; i++){
            StringTokenizer st = new StringTokenizer(br.readLine());
            int sum = 0;

            while (st.hasMoreTokens()) {
                sum += Integer.parseInt(st.nextToken());
            }

            sb.append(arr[sum]).append("\n");
        }

        bw.write(sb.toString());
        bw.close();
    }
}
```
    
위에서 말했듯이 1의 개수를 세는것과 배열의 전체 합의 값이 동일함.  


> arr[0] = 0, 0, 0, 0 윷(D)  
> arr[1] = 0, 0, 0, 1 걸(C)  
> arr[2] = 0, 0, 1, 1 개(B)  
> arr[3] = 0, 1, 1, 1 도(A)  
> arr[4] = 1, 1, 1, 1 모(E)  
    
