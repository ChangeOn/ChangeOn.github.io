> **섹션 3. 정렬 (Updated)**
+ 합병정렬 (merge sort)
    ```java
    // O(N)
    void merge(int data[], int p, int q, int r) {
        int i=p, j=q+1, k=p;
        int tmp[data.length()];

        while(i<=q && j<=r){
            if(data[i] <=data[j]>) {
                tmp[k++]=data[i++];
            }else {
                tmp[k++]=data[j++];
            }
        }

        while(i<=q) {
            tmp[k++]=data[i++];
        }
        while(i<=r) {
            tmp[k++]=data[j++];
        }

        for(int i=p; i<=r; i+++){
            data[i]=tmp[i];
        }
    }
    ```

+ 빠른정렬 (quicksort)
    ```java
    quickSort(A[], p, r) {
        if(p<r) {
            q = partition(A[], p, r);
            quickSort(A[], p, q-1);
            quickSort(A[], q+1, r);
        }
    }

    partition(A[], p, r) {
        int x = A[r];
        int i = p-1;
        for (int j=p; j<r-1; j++){
            if(A[j] <= x) {
                i = i+1;
                exchange A[i] and A[j];
            }
        }
        exchange A[i+1] and A[r];
        return i+1;
    }
    ```
+ 힙 정렬 (heap sort)
    ```java
    public class Heap {
        // MAX-HEAPIFY : 트리 전체를 heap으로 만드는 기본 연산
        // pseudo code
        void maxHeapify(int [] A, int i) {
            if(!child of A[i]){
                return;
            }
            int k = index of the biggest child of A[i];
            if(A[i] >= A[k]){
                return;
            }
            exchange A[i] and A[k];
            maxHeapify(A, k);
        }

        // iterative version
        void maxHeapify2(int [] A, int i) {
            while(child of A[i]){
                int k = index of the biggest child of A[i];
                if(A[i] >= A[k]){
                    return;
                }
                exchange A[i] and A[k];
                i = k;
            }
        }

        // 정렬할 배열을 힙으로 만들기
        // pseudo code
        BUILD-MAX-HEAP (A)
        int heap-size[A] = length[A]
        for (i = length[A]/2; i>=1; i--) {
            MAX-HEAPIFY(A, i);
        }
        
        void heapSort(A) {
            BUILD-MAX-HEAP(A);
            for(i = heap_size; i>=2; i--){
                exchange A[1] and A[i];
                heap_size = heap_size - 1;
                maxHeapify(A, 1);
            }
        }

        <!-- 힙(heap)의 다른 응용 : 우선순위 큐 (priority qeueu)-->
        // 1. INSERT(x)
        MAX-HEAP-INSERT(A, key) {
            heap_size = heap_size + 1;
            A[heap_size] = key;
            i = heap_size;
            while (i>1 && A[PARENT(i)] < A[i]>) {
                exchnage A[i] and A[PARENT(i)];
                i = PARENT(i);
            }
        }

        // 2.EXTRACT_MAX()
        int heapExtractMax(int[] A) {
            if (heap-size[A] < 1) {
                System.out.println("heap underflow");
                return;
            }
            int max = A[1];
            A[1] = A[heap-size[A]];
            heap-size[A] = heap-size[A] - 1;
            maxHeapify(A, 1);
            return max;
        }
    }
    ```
    + **Sorting in Linear Time** \
    **1. Comparision Sort** \
    **2. 선형시간 정렬 알고리즘**
        - Counting Sort
        ```java
        // Counting sort (non-comparision sort)
            // ⬇ 레코드의 일부만 정렬하게 됨
            int A[n];
            int C[k] = {0, };
            for (int i=1; i<=n; i++) {
                C[A[i]]++;
            }
            for(int s=1, i=0; i<=k; i++) {
                for(int j=0; j<C[i]; j++) {
                    A[s++] = i;
                }
            }

            // pseudo code
            COUNTING-SORT(A, B, k)
            for (int i=0; i<=k; i++) {
                C[i] = 0;
            }
            for (int j=0; j>=A.length; j++) {
                C[A[j]] = C[A[j]] + 1;
            }
            for(int i=1; i<=k; i++) {
                C[i] = C[i] + C[i-1];
            }
            for(int j=A.length; j>=0; j--){
                B[C[A[j]]] = A[j];
                C[A[j]] = C[A[j]] - 1;
            }
        ```
    + **Sorting in Linear Time : Radix Sort**
        ```java
        // Radix sort (non-comparision)
            RADIX-SORT(A, d)
            for (int i=1; i<=d; i++){
                use a stable sort to array A on digit i;
            }
        ```