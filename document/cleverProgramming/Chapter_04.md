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