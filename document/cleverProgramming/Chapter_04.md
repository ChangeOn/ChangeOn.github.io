> **섹션 5. 검색트리 - 레드블랙트리**
+ red black tree - 1
    ```java
        LEFT-ROTATE(T, x){
            int y = right[x];   // y 초기화
            right[x] = left[y]; // y의 왼쪽 부트리를 x의 오른쪽 부트리로 전환.
            p[left[y]] = x;
            p[y] = p[x];    // x의 부모노드와 y를 연결한다.
            
            if(p[x] == NIL[T]){
                root[T] = y;
            }else if(x == left[p[x]]){
                left[p[x]] = y;
            }else {
                right[p[x]] = y;
            }
            left[y] = x;
            p[x] = y;
            
        }
    ```
    > `레드-블랙 트리의 정의`  
     다음 조건을 만족하는 이진탐색트리
     1. 각 노드는 red 혹은 black 이고,  
     2. 루트노드는 black
     3. 모든 리프노드(즉, NTL노드)는 black이며  
     4. red노드의 자식노드들은 전부 black (즉, red노드는 연속되어 등장하지 않음)  *red-red violation  
     5. 모든 노드에 대해서 그 노드로부터 자손인 리프노드에 이르는 모든 경로에는 동일한 개수의 black노드가 존재한다. *BH:black height


+ red black tree - 2 (INSERT)
    ```java
        RedBlack-INSERT(T, z){
            y = null;   // x를 -1로 따라가는 pointer. (z가 삽입될 위치)
            x = root[T];
            while(x != null) {
                y = x;
                if(key[z] < key[y]>){
                    x = left[x];
                }else {
                    x = right[x];
                }
            }
            p[z] = y;
            if(y == null){
                root{T} = z;
            }else if(key[z] < key[y]){
                left[y] = z;
            }else {
                right[y] = z;
            }
            <!-- 여기까지 일반 BST처럼 노드를 INSERT -->

            left[z] = null;
            right[z] = null;
            color[z] = RED; // 새로운 노드 z를 red노드로 한다.
            RedBlack-INSERT-FIXUP(T, z);
        }

        // Case 1,2,3 : z의 부모노드가 p[p[z]]의 왼쪽 자식일 경우
        // Case 4,5,6 : z의 부모노드가 p[p[z]]의 오른쪽 자식일 경우
        RedBlack-INSERT-FIXUP(T, z){
            while(p[z] !=null && color[p[z]] == RED){
                if(p[z] == left[p[p[z]]]) {
                    y = right[p[p[z]]];
                    if(color[y] == RED){    // Case1: z의 삼촌이 red노드
                        color[p[z]] = BLACK;    
                        color[y] = BLACK;
                        color[p[p[z]]] = RED;
                        z = p[p[z]];
                    }else if(z == right[p[z]]){ // Case2,3: z의 삼촌이 black노드
                        z = p[z];
                        LEFT-ROTATE(T, z);  //---Case2: z가 오른쪽 자식일 경우, LEFT-ROTATE
                    }
                    // Case3: z가 왼쪽 자식일 경우
                    color[p[z]] = BLACK;
                    color[p[p[z]]] = RED;
                    RIGHT-ROTATE(T, p[p[z]]);
                }else {
                    // Case 4,5,6의 경우 위 then절에서 왼쪽-오른쪽만 바뀌고 나머지 모두 동일 
                    y = left[p[p[z]]];
                    if(color[y] == RED){
                        color[p[z]] = BLACK;    
                        color[y] = BLACK;
                        color[p[p[z]]] = RED;
                        z = p[p[z]];
                    }else if(z == left[p[z]]){
                        z = p[z];
                        RIGHT-ROTATE(T, z);
                    }
                    color[p[z]] = BLACK;
                    color[p[p[z]]] = RED;
                    LEFT-ROTATE(T. p[p[z]]);
                }
            }
            color[root[T]] = BLACK; // root가 RED인 채로 while문이 종료될 경우가 있으므로 BLACK으로 바꿔줌.
        }
    ```

+ red black tree - 3 (DELETE)
    ```java
        RB-DELETE(T, z){
            if(left[z] === null || right[z] === null){
                y = z;
            }else {
                y = TREE-SUCCESSOR(z);
            }

            if(left[y] != null){
                x = left[y];
            }else{
                x = right[y];
            }

            p[x] = p[y];
            if(p[y] == null){
                root[T] = x;
            }else if(y == left[p[y]]){
                left[p[y]] = x;
            }else {
                right[p[y]] = x;
            }

            if(y != z){
                key[z] = key[y];    // y의 satellite data를 z로 복사
            }

            if(color[y] == BLACK){
                RB-DELETE-FIXUP(T, x)
            }

            return y;
        }

        RB-DELETE-FIXUP(T, x){
            while(x != root[T] && color[x] == BLACK){
                if(x == left[p[x]]){
                    w = right[p[x]];    // w = x의 형제노드
                    if(color[w] == RED){
                        <!-- Case1: x가 부모늬 왼쪽 자식이고, w가 RED인 경우 -->
                        color[w] == BLACK;
                        color[p[x]] = RED;
                        LEFT-ROTATE(T, p[x]);
                        w = right[p[x]];
                    }
                    if(color[left[w]] == BLACK && color[right[w]] == BLACK){
                        <!-- Case2: 〃, w와 w의 자식들이 BLACK인 경우 -->
                        color[w] = RED;
                        x = p[x];
                    }else if(color[right[w] == BLACK]){
                        <!-- Case3: 〃, w는 BLACK, w의 왼쪽자식이 RED인 경우 -->
                        color[left[w]] = BLACK;
                        color[w] = RED;
                        RIGHT-ROTATE(T, w);
                        w = right[p[x]];
                        <!-- Case4: 〃, w는 BLACK, w의 오른쪽자식이 RED인 경우 -->
                        color[w] = color[p[x]];
                        color[p[x]] = BLACK;
                        color[right[w]] = BLACK;
                        LEFT-ROTATE(T, p[x]);
                        x = root[T];
                    }
                }else {
                    // x == right[p[x]]인 경우 (Case 4,5,6,7,8)
                    // same as then clause with "right" and "left" exchange
                }
            }
            color[x] = BLACK;
        }
    ```