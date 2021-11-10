> **섹션 4. 검색트리 - 이진검색트리**
+ 트리와 이진트리
    - 이진트리 순회 (Inorder, Preorder, Postorder, Level-order)
    ```java
        // binary tree traversal
        // 중순위(Inorder)
        INORDER-TREE-TRAVERSAL(x) { // x: 루트노드
            if (x != null) {
                INORDER-TREE-TRAVERSAL(left[x]);
                print(key[x]);
                INORDER-TREE-TRAVERSAL(right[x]);
            }
        }
        // 선순위(Preorder)
        // 후순위(Postorder)

        // Level-Order 순회
        LEVEL-ORDER-TRAVERSAL() {
            visit the root;
            Q = root;
            while (Q != null) {
                v = dequeue(Q);
                visit children of v;
                enqueue children of v into Q;
            }
        }
    ```
+ 이진검색트리(Binary Search Tree)
    - SEARCH, INSERT, DELETE
    ```java
    // Dynamic Set
        // SEARCH
        TREE-SEARCH(x, k){
            if(x==null || k==key[x]){
                return x;
            }
            if(k < key[x]){
                return TREE-SEARCH(left[x], k);
            }else {
                return TREE-SEARCH(right[x], k);
            }
        }
        // Iterative Version
        ITERATIVE-TREE-SEARCH(x, k){
            while(x != null && k != key[x]){
                if(k<key[x]){
                    x = left[x];
                }else {
                    x = right[x];
                }
            }
            return x;
        }
        
        TREE-MINIMUN(x){
            while(left[x] != null){
                x = left[x]
            }
            return x;
        }
        TREE-MAXIMUM(x){
            while(right[x] != null){
                x = right[x]
            }
            return x;
        }
        TREE-SUCCESSOR(x){
            if(right[x] != null){
                return TREE-MINIMUN(right[x];)
            }
            int y = p[x];
            while(y != null && x == right[y]){
                x = y;
                y = p[y];
            }
            return y;
        }

        // INSERT
        TREE-INSERT(T, z){
            y = null;
            x = root[T];
            while(x != null){
                y = x;
                if(key[z] < key[x]){
                    x = left[x];
                }else {
                    x = right[x];
                }
            }
            p[z] = y;
            if(y == null){
                root[T] = z;
            }else if(key[z] < key[y]){
                left[y] = z;
            }else {
                right[y] = z;
            }
        }

        // DELETE
        TREE-DELETE(T, z){
            if(left[z] == null || right[z] == null){
                y = z;
            }else {
                y = TREE-SUCCESSOR(z);
            }
            if(left[y] != null){
                x = left[y];
            }else {
                x = right[y];
            }
            if(x != null){
                p[x] = p[y];
            }
            if(p[y] == null){
                root[T] = x;
            }else if(y == left[p[y]]){
                left[p[y]] = x;
            }else {
                right[p[y]] = x;
            }

            if(y != z){
                key[z] = key[y];
                // copy y's satellite data into z
            }
            return y;
        }
    ```