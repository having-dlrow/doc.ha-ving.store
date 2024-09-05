# DFS/BFS

\[ 문제 ] Graph 알고리즘을 설명해주세요. Graph 알고리즘에서 구현 가능한가요?

\[ 정답 ]

### Graph 알고리즘

#### 개념

1. 노드와 간선(Edge) 구성된 자료구조

#### 구성

| 노드(정점) | 어떤 객체나 위치                       |
| ------ | ------------------------------- |
| 간선     | 두 노드 간의 연결 선                    |
| 방향     | A→ B ( A에서 B 연결 O, B에서 A 연결 X ) |
| 가중치    | 간선을 통과하는데 드는 비용                 |

#### 종류

**그래프 탐색 알고리즘**

<figure><img src="../../../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

*   **너비(Beneath) 우선탐색**

    * 큐 구현

    ```java
    // 1 부터 출발 
    // + 인접노드정보 : 다음 대상
    // + 방문 여부(테이블 혹은 노드속성) : 제외 값
    // + 방문 예정 큐 : 저장 용
    Node root;
    root.visited = true;

    Queue queue = new LinkedList<Node>();
    queue.add(root);

    while (!queue.isEmpty()) {
    		Node currentNode = queue.remove();
    		
    		currentNode.visited = true;
    		visit();               // 방문함.
    		
        for (node n : currentNode.adjacent) {
            if (n.visited == false)
                queue.add(n)
        }
    }
    ```
*   **깊이(Depth) 우선탐색**

    * 재귀로 구현

    ```java
    // 1부터 출발
    // + 인접노드정보 : 다음 대상
    // + 방문 여부(테이블 혹은 노드속성) : 제외 값

    function dfs(Node currentNode) {
    	if(currentNode == null) return;

    	 currentNode.visit= true;	
    	 visit();                // 방문함.

    	for(node n : currentNode.adjacent) {
    			if(n.visited == false)
    			    dfs(n);
    	}
    } 

    ```

**최단 경로 알고리즘**

* 다익스트라
* 벨만-포드
* 플로이드
