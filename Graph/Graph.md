
# ⛳ Objective

_그래프 관련 개념들을 복습하기 위한 문서이다. 자주 사용되는 그래프 개념들과 Python을 이용한 구현방식에 대해서 정리하였다._

- 그래프의 정의와 종류에 대해서 알아본다.
- 그래프를 표현하는 방식에 대해서 알아본다.
- 그래프 탐색에 대해서 알아본다.

# ☑️ 그래프(Graph)

<img src="https://github.com/woody35545/Algorithm-study/assets/84436996/4f125e35-b71c-40f8-981a-4c44f1e1b9ab" width="30%" height="40%">


그래프는 노드(또는 정점(vertex))와 간선(Edge)으로 구성된 자료구조로 객체들이 어떠한 관계를 가지고 연결되어 있을 때 이를 표현하기 위한 자료구조이다.

- **Vertex(또는 Node):** 그래프에서 특정 객체를 나타내는 자료의 단위이다.
- **Edge:** 두 vertex 사이를 연결 관계를 표시하기 위한 선이다. 출발하는 정점과 도착하는 정점의 쌍(u,v)으로 표현한다.
    - 방향성 간선(Directed Edge)과 무방향성 간선(Undirected Edge)이 있다.

# ☑️ 그래프의 종류

## 📌 방향성 **그래프 / 무방향성 그래프**

### **방향성 그래프(Directed Graph)**

- 방향성 그래프는 간선에 방향이 존재하는 그래프이다.
- 간선에 방향에 따라 노드간 참조가 제약을 받는다.

### **무방향성 그래프(Undirected Graph)**

- 무방향성 그래프는 간선에 방향이 존재하지 않는 그래프이다.
- 간선으로 연결된 모든 노드들이 양방향 참조가 가능하다.
- 모든 간선이 양방향 간선이라고 생각하면 된다.

## 📌 **연결 그래프 / 비연결 그래프**

### **연결 그래프**

- 그래프에 존재하는 임의의 두 노드 사이에 접근 가능한 경로가 반드시 존재하면 연결 그래프이다.

### **비연결 그래프**

- 그래프에 존재하는 임의의 두 노드 사이에 접근 가능한 경로가 존재하지 않는 경우가 하나라도 존재하는 경우 비연결 그래프이다.

## 📌 **가중치 그래프(Weighted Graph)**

- 가중치나 비용은 노드 사이의 연결뿐만 아니라 연결에 필요한 비용도 같이 반영하고 싶을 때 사용된다.
- 그래프의 각 간선이 비용 또는 가중치를 가지는 그래프를 가중치 그래프라고 한다.
- 가중치 그래프와 관련된 대표적인 자료구조는 MST(Minimum Spanning Tree)가 있고, 알고리즘으로는 Kruskal과 Prim 알고리즘이 있다.
    - 신장트리(Spanning Tree)란 그래프의 최소 연결 부분 그래프이다.
    - MST란, 어떤 그래프의 신장 트리 중에서 사용된 간선들의 가중치 합이 최소인 신장 트리이다.
    - MST를 구하는 알고리즘에는 Kruskal과 Prim 알고리즘이 있다.

 

## 📌 **완전 / 부분 그래프**

### **완전 그래프(Complete Graph)**

- 그래프의 모든 정점들이 서로 연결되어 있는 그래프를 완전 그래프라고 한다.

### 부분 그래프(Sub Graph)

- 특정 그래프를 이루는 Vertex와 Edge 중 일부를 사용해서 만들 수 있는 그래프는 부분 그래프이다.
- 엄밀한 정의는 다음과 같다. 
G = (V,E)의 부분 그래프는 V’⊆V이고 E’⊆E 인 G’ = (V’,E’)은 G의 서브 그래프이다.

## 📌 **순환 / 비순환 그래프**

### 순환(Cycle) 그래프

  - 한 Vertex에서 시작해서 여러 경로를 거쳐 다시 해당 Vertex로 돌아올 수 있다면 순환 그래프이다. 이러한 순환 경로를 Cycle이라고 한다.

### 비순환(Acycle) 그래프
  - 순환하는 경로가 없는 그래프를 비순환 그래프라고 한다.
  - 즉 사이클이 없는 그래프이다.

# ☑️ 그래프의 표현

- 구현의 관점에서 그래프를 표현하는 여러 자료구조와 방식들에 대해 설명한다.

## 📌 **인접 리스트(Adjacency List)로 표현**
```python
# 5개 노드의 인접 노드 정보를 담을 인접 리스트 

SIZE = 5

adjList = [[] for _ in range(SIZE)]

print(adjList) 
"""
  [[],
   [],
   [],
   [],
   []]
"""
```

**언제 사용하나?** 

- 그래프가 희소한(Sparse) 경우 사용한다.
- 간선에 비해 노드의 개수가 상대적으로 많은 경우 유리하다.

**장점**

- 각 노드에 연결된 간선들을 리스트로 표현하기 때문에 연결된 간선을 찾는데 O(degree)의 시간이 소요되므로, 정점의 이웃을 빠르게 탐색 가능하다.
- 메모리를 효율적으로 사용한다.

**단점**

- 인접 행렬방식에 비해서 특정 두 정점 간의 연결여부를 찾는 속도가 느리다.

## 📌 **인접 행렬(Adjacency Matrix)로 표현**
```python
# 0으로 초기화 된 5x7 Matrix 생성

ROW_SIZE = 5
COL_SIZE = 7

adjMatrix = [[0 for _ in range(COL_SIZE)] for _ in range(ROW_SIZE)] 
print(adjMatrix)
"""
  [[0, 0, 0, 0, 0, 0, 0],
   [0, 0, 0, 0, 0, 0, 0],
   [0, 0, 0, 0, 0, 0, 0], 
   [0, 0, 0, 0, 0, 0, 0], 
   [0, 0, 0, 0, 0, 0, 0]]
"""

```

**언제 사용하나?**

- 그래프가 밀집한 경우(Dense Graph) 인접 행렬이 유용하다.
- 그래프를 구성하는 간선의 수가 정점의 수보다 상대적으로 많을 때 사용한다.
- 미로 찾기와 같이 주어지는 노드들의 구조가 격자 형태의 구조를 가질때 인접행렬로 표현하면 직관적이고 편하다.

**장점**

- 특정 두 정점간의 연결 여부를 상수 시간(O(1))에 알 수 있다.
- 직관적인 표현을 할 수 있다.

**단점**

- 노드의 수에 비례하여 메모리 자원을 많이 소모하게 된다.
- 그래프가 희소한 경우 사용되지 않는 메모리가 많아져서 불필요한 메모리 낭비가 발생할 수 있다.

## 📌 **엣지 리스트(Edge List)로 표현**

# ☑️ 그래프 탐색(Graph traversal)

- 그래프 탐색이란, 그래프 자료구조에서 모든 정점을 방문하거나 원하는 조건을 만족하는 정점을 찾아가기 위한 행위를 의미한다.
- 그래프 탐색을 위한 방법에는 DFS와 BFS가 있다.

## 📌 그래프 탐색 알고리즘

### 깊이 우선 탐색(DFS)

- DFS는 출발 노드에서부터 시작해서 가장 깊은 곳을 우선적으로 탐색하는 알고리즘이다.
- 한길만 쭉 파는 방식이다. 가장 깊은곳까지 도달해서 경로가 끝나야만 다른 경로를 탐색한다.
- Stack으로 구현한다.

### 너비 우선 탐색(BFS)

- 너비 우선 탐색은 출발 노드로부터 가까운 지점부터 탐색한다.
- 가까운 대상부터 방문하기 때문에 먼저 찾아진 경로가 항상 최단경로이다. 따라서 최단 경로를 찾을 때 유리하다.
- Queue로 구현한다.