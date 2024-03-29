> **섹션 2. 순환 (Recursion)**
+ Reursion 응용 - 미로 1
    ```java
    public class Maze {
        private static int N = 8;
        private static int [][] maze = {
            {0,0,0,0,0,0,0,1},
            {0,1,1,0,1,1,0,1},
            {0,0,0,1,0,0,0,1},
            {0,1,0,0,1,1,0,0},
            {0,1,1,1,0,0,1,1},
            {0,1,0,0,0,1,0,1},
            {0,0,0,1,0,0,0,1},
            {0,1,1,1,0,1,0,0}
        };

        private static final int PATHWAY = 0;
        private static final int WALL = 1;
        private static final int BLOCKED = 2; // visited && 경로X
        private static final int PATH = 3;  // visited && 경로?

        public static boolean findMazePath(int x, int y) {
            if(x<0 || y<0 || x>=N || y>=N) {
                return false;
            }else if(maze[x][y] != PATHWAY) {
                return false;
            }else if(x == N-1 && y == N-1){
                maze[x][y] = PATH;
                return true;
            }else {
                maze[x][y] = PATH;
                if(findMazePath(x-1, y) || findMazePath(x, y+1) || findMazePath(x+1, y) || findMazePath(x1, y-1)) {
                    return true;
                }
                maze[x][y] = BLOCKED;
                return false;
            }
        }

        public static void main(String[] args) {
            findMazePath(0,0);
        }
    }
    ``` 

+ Recursion 응용 - Counting Cells in a Blob
    ```java
    public class Blob {
        private static int N = 8;
        private static int [][] grid = {
        //     {0,0,0,0,0,0,0,1},
        //     {0,1,1,0,1,1,0,1},
        //     {0,0,0,1,0,0,0,1},
        //     {0,1,0,0,1,1,0,0},
        //     {0,1,1,1,0,0,1,1},
        //     {0,1,0,0,0,1,0,1},
        //     {0,0,0,1,0,0,0,1},
        //     {0,1,1,1,0,1,0,0}
        };

        private static final int BACKGROUND_COLOR = 0;
        private static final int IMAGE_COLOR = 1;
        private static final int ALREADY_COUNTED = 2;

        public static int countCells(int x, int y) {
            if (x<0 || x>=N || y<0 || y>=N) {
                return 0;
            }else if (grid[x][y] != IMAGE_COLOR) {
                return 0;
            }else {
                grid[x][y] = ALREADY_COUNTED;
                return 1 + countCells(x-1, y) + countCells(x-1, y+1) + countCells(x, y+1)
                    + countCells(x+1, y+1) + countCells(x+1, y) + countCells(x+1, y-1)
                    + countCells(x, y-1) + countCells(x-1, y-1);
            }
        }

        public static void main(String[] args) {
            countCells(0,0);
        }
    }
    ```

+ Recursion의 응용 - n queens problem
    ```java
    public class Queens {

        int [] cols new int [N+1];
        public static boolean queens(int level) {
            if(!promising(level)) {
                return false;
            } else if(level == N) {
                for (int i=1; i<=N; i++) {
                    System.out.println("("+i+", "+cols[i]+")");
                }
                return true;
            } else {
                for(int i=1; i<=N; i++) {
                    cols[level+1] = i;
                    if(queens(level+1)) {
                        return true;
                    }
                }
                return false;
            }
        }

        public static boolean promising(int level) {
            for(int i=1; i<level; i++) {
                if(cols[i] == cols[levet]) {
                    return false;
                } else if (level-i == Math.abs(cols[level]-cols[i])) {
                    return false;
                }
            }
            return true;
        }
    }
    ```

+ 멱집합 (powerset)
    ```java
    private static char data[] = {'a','b','c','d','e','f'};
    private static int n = data.length;
    private static boolean [] include = new boolean [n];
                            // ⬆, ⬇ : 상태공간 트리에서 현재 나의 위치를 표현한다.
    public static void powerSet(int k) {
        if (k==n) {     // 만약 현재 내 위치가 리프노드라면
            for(int i=0; i<n; i++) {
                if(include[i]) {
                    System.out.print(data[i] + " ");
                    System.out.println();
                    return;
                }
            }
        }

        include[k]=false;
        powerSet(k+1);      // 먼저 왼쪽으로 내려갔다가
        include[k]=true;
        powerSet(k+1);      // 오른쪽으로 내려간다.
    }

    public static void main(String[] args) {
        // 처음 호출할 때는 powerSet(0)로 한다. 즉 P는 공집합이고, S는 전체집합
        powerSet(0);
    }
    ```