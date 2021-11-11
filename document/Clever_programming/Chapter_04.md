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