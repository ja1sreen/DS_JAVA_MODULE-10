# Ex21 Count the Number of Nodes in the Left Subtree of a Binary Tree
## DATE: 28.08.2026
## AIM:
To design and implement a java program that constructs a binary tree from given level order input and counts the number of nodes present in the left subtree of the root node

## Algorithm
1. Start the program.
2. Read integer.
3. Create an array of size n.
4.  Read n integers and store them in array.
5.   Building the Tree (Level-Order).
6. Counting Left Subtree Nodes.
7. Print the result.
8. Stop the program.  

## Program:
```
/*
Program to constructs a binary tree from given level order input and counts the number of nodes 
Developed by: JAISREE N
RegisterNumber: 212224060104
*/
```
```
import java.util.*;

class Node {
    int data;
    Node left, right;

    Node(int data) {
        this.data = data;
        left = right = null;
    }
}

public class Main {

    static Node buildTree(int[] arr) {
        if (arr.length == 0) return null;

        Node root = new Node(arr[0]);
        Queue<Node> queue = new LinkedList<>();
        queue.add(root);

        int i = 1;
        while (i < arr.length) {
            Node current = queue.poll();

            if (i < arr.length) {
                current.left = new Node(arr[i++]);
                queue.add(current.left);
            }

            if (i < arr.length) {
                current.right = new Node(arr[i++]);
                queue.add(current.right);
            }
        }
        return root;
    }

    static int count(Node root) {
        if (root == null) return 0;
        return 1 + count(root.left) + count(root.right);
    }

    static void countNodes(Node root) {
        if (root == null || root.left == null) {
            System.out.println(0);
            return;
        }
        System.out.println(count(root.left));
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int[] arr = new int[n];

        for (int i = 0; i < n; i++)
            arr[i] = sc.nextInt();

        Node root = buildTree(arr);
        countNodes(root);
    }
}
```

## Output:
<img width="396" height="278" alt="image" src="https://github.com/user-attachments/assets/679c6749-21ed-495f-b157-3d2a5995ff3e" />

## Result:
The program has been successfully implemented and executed.
It correctly constructs the binary tree from level order input and counts the number of nodes in the left subtree of the root node.

# Ex22 Searching for a Book ID in a Binary Search Tree (BST)
## DATE: 28.08.2026
## AIM:
To design and implement java program that constructs a Binary Search Tree (BST) using given Book IDs and checks whether a specific Book ID exists in the BST.
1. Start the program.
2. Read integer.
3. Initialize root equals to null.
4. Repeat n times.
5. Insert(root, key).
6. Searching Book ID.
7. Search(root, key).
8.  Stop the program.   

## Program:
```
/*
Program to constructs a Binary Search Tree (BST) using given Book IDs 
Developed by: JAISREE N
RegisterNumber: 212224060104
*/
```
```
import java.util.*;

public class PatientBST {

    public static Node insert(Node root, int key) {
        if (root == null)
            return new Node(key);

        if (key < root.data)
            root.left = insert(root.left, key);
        else if (key > root.data)
            root.right = insert(root.right, key);

        return root;
    }

    public static Node delete(Node root, int key) {
        if (root == null)
            return null;

        if (key < root.data) {
            root.left = delete(root.left, key);
        } 
        else if (key > root.data) {
            root.right = delete(root.right, key);
        } 
        else {
            // Node with one child or no child
            if (root.left == null)
                return root.right;
            else if (root.right == null)
                return root.left;

            // Node with two children
            Node successor = findMin(root.right);
            root.data = successor.data;
            root.right = delete(root.right, successor.data);
        }
        return root;
    }

    private static Node findMin(Node root) {
        while (root.left != null)
            root = root.left;
        return root;
    }

    public static void inorder(Node root) {
        if (root == null)
            return;

        inorder(root.left);
        System.out.print(root.data + " ");
        inorder(root.right);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        Node root = null;

        for (int i = 0; i < n; i++) {
            root = insert(root, sc.nextInt());
        }

        int del = sc.nextInt();
        root = delete(root, del);

        inorder(root);
    }
}

class Node {
    int data;
    Node left, right;

    Node(int data) {
        this.data = data;
        left = right = null;
    }
}
```

## Output:
<img width="528" height="296" alt="image" src="https://github.com/user-attachments/assets/8b9e13c2-2d67-4e37-bb4c-f2cb65e0a0ab" />

## Result:
The program has been successfully implemented and executed.
It constructs a Binary Search Tree from the given Book IDs and accurately determines whether a queried Book ID exists in the library system.

# Ex23 Breadth-First Search (BFS) Traversal of a City Junction Map
## DATE: 28.08.2026
## AIM:
To design and implement a java program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph, and find all reachable locations from a given source junction.
## Algorithm
1. Start the program.
2. Read two integers.
3. Create an adjacency list g of size n.
4. Repeat e times.
5. Read the source node.
6. Initialize a boolean array of size n, all set to false.
7. Create an empty queue.
8. Mark src as visited and enqueue it.
9. Continue until all reachable nodes are processed.
10. Stop the program.

## Program:
```
/*
Program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph
Developed by: JAISREE N
RegisterNumber: 212224060104
*/
```
```
import java.util.*;

public class EmergencyRouteBFS {

    public static void addEdge(List<List<Integer>> g, int u, int v) {
        g.get(u).add(v);
        g.get(v).add(u); // Undirected graph
    }

    public static void bfs(List<List<Integer>> g, int src, boolean[] visited) {
        Queue<Integer> queue = new LinkedList<>();

        visited[src] = true;
        queue.add(src);

        while (!queue.isEmpty()) {
            int current = queue.poll();
            System.out.print(current + " ");

            for (int neighbor : g.get(current)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
                }
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(), e = sc.nextInt();
        List<List<Integer>> g = new ArrayList<>();

        for (int i = 0; i < n; i++)
            g.add(new ArrayList<>());

        for (int i = 0; i < e; i++)
            addEdge(g, sc.nextInt(), sc.nextInt());

        int src = sc.nextInt();
        bfs(g, src, new boolean[n]);
    }
}
```

## Output:
<img width="470" height="373" alt="image" src="https://github.com/user-attachments/assets/c8ae4ece-0d8d-4612-b85c-d30c5557c3f5" />

## Result:
The program has been successfully implemented and executed.
It performs Breadth-First Search (BFS) traversal on a city junction map and correctly lists all reachable locations from the given source node.

# Ex24 Shortest Path and Reachability in a Heritage Town using BFS
## DATE: 28.08.2026
## AIM:
To design and implement a java program that, given a map of attractions in a heritage town connected by walking paths, recommends:
The shortest number of paths (minimum hops) from a starting attraction to a target attraction.
The number of reachable attractions from the same starting point using Breadth-First Search (BFS)


## Algorithm
1. Start the program.
2. Read integers.
3. Create an adjacency list graph of size n.
4. Build the Graph.
5. Read Start and Target.
6. Initialize BFS.
7. Initialize DFS
8. Counting Reachable Attractions and Print.
9. End the program.  

## Program:
```
/*
Program to determine Shortest Path and Reachability in a Heritage Town using BFS
Developed by: JAISREE N
RegisterNumber: 21224060104
*/
```
```
import java.util.*;

public class TouristNavigation {
    
    public static int shortestPath(List<List<Integer>> graph, int start, int target, int n) {
        
        boolean[] visited = new boolean[n];
        int[] distance = new int[n];
        Queue<Integer> queue = new LinkedList<>();

        visited[start] = true;
        queue.add(start);
        distance[start] = 0;

        while (!queue.isEmpty()) {
            int node = queue.poll();

            if (node == target)
                return distance[node];

            for (int neighbor : graph.get(node)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    distance[neighbor] = distance[node] + 1;
                    queue.add(neighbor);
                }
            }
        }

        return -1; // unreachable
    }

    public static void reachableAttractions(List<List<Integer>> graph, boolean[] visited, int node) {
        visited[node] = true;

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                reachableAttractions(graph, visited, neighbor);
            }
        }
    }

    public static int countReachable(boolean[] visited) {
        int count = 0;
        for (boolean v : visited) {
            if (v) count++;
        }
        return count;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(), e = sc.nextInt();
        List<List<Integer>> graph = new ArrayList<>();

        for (int i = 0; i < n; i++)
            graph.add(new ArrayList<>());

        for (int i = 0; i < e; i++) {
            int u = sc.nextInt(), v = sc.nextInt();
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        int start = sc.nextInt();
        int target = sc.nextInt();

        int shortest = shortestPath(graph, start, target, n);

        boolean[] visited = new boolean[n];
        reachableAttractions(graph, visited, start);
        int reachable = countReachable(visited);

        System.out.println("Shortest path from start to target: " + shortest);
        System.out.println("Total reachable attractions from start: " + reachable);
    }
}
```

## Output:
<img width="1185" height="382" alt="image" src="https://github.com/user-attachments/assets/6b74ef81-43a4-46dc-a831-4766feafbfcc" />

## Result:
The program has been successfully implemented and executed.
It correctly computes:
The shortest number of paths (minimum hops) between two attractions.
The total number of reachable attractions from a given starting point using BFS traversal.

# Ex25 Finding the Fastest Route to a Charging Station using Dijkstra’s Algorithm
## DATE: 28.08.2026
## AIM:
To design and implement a java program that helps an electric vehicle (EV) find the shortest travel time from its current block to the nearest charging station using Dijkstra’s shortest path algorithm.
## Algorithm
1. Start the program.
2. Read integers.
3. Create an adjacency list graph of size n, where each node stores a list of (neighbor, time) pairs.
4. Build the Graph.
5. Read Remaining Input.
6. Initialize Dijkstra’s setup.
7. Dijkstra’s Relaxation Loop.
8. Find minimum time among stations.
9. End the program.
    
## Program:
```
/*
Program to find the Fastest Route to a Charging Station using Dijkstra’s Algorithm
Developed by: JAISREE N
RegisterNumber: 212224060104
*/
```
```
import java.util.*;

public class EVChargingNavigation {

    static class Pair {
        int node, time;
        Pair(int node, int time) {
            this.node = node;
            this.time = time;
        }
    }

    static int findNearestChargingStation(int n, List<List<Pair>> graph, int source, Set<Integer> stations) {

        int[] dist = new int[n];
        Arrays.fill(dist, Integer.MAX_VALUE);

        PriorityQueue<Pair> pq = new PriorityQueue<>(Comparator.comparingInt(p -> p.time));

        dist[source] = 0;
        pq.add(new Pair(source, 0));

        while (!pq.isEmpty()) {
            Pair current = pq.poll();
            int node = current.node;
            int time = current.time;

            // If this node is a charging station, return its distance
            if (stations.contains(node)) {
                return time;
            }

            if (time > dist[node]) continue;

            for (Pair neighbor : graph.get(node)) {
                int newDist = dist[node] + neighbor.time;

                if (newDist < dist[neighbor.node]) {
                    dist[neighbor.node] = newDist;
                    pq.add(new Pair(neighbor.node, newDist));
                }
            }
        }

        return -1; 
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(), m = sc.nextInt();
        List<List<Pair>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        for (int i = 0; i < m; i++) {
            int u = sc.nextInt(), v = sc.nextInt(), w = sc.nextInt();
            graph.get(u).add(new Pair(v, w));
            graph.get(v).add(new Pair(u, w)); // Undirected
        }

        int source = sc.nextInt();
        int k = sc.nextInt();
        Set<Integer> stations = new HashSet<>();
        for (int i = 0; i < k; i++) stations.add(sc.nextInt());

        System.out.println(findNearestChargingStation(n, graph, source, stations));
    }
}
```

## Output:
<img width="460" height="465" alt="image" src="https://github.com/user-attachments/assets/eb94a482-3713-4781-aafa-cc86ae09a64f" />

## Result:
The program has been successfully implemented and executed.
It uses Dijkstra’s algorithm to determine the shortest travel time from the EV’s current location to the nearest charging station and correctly handles cases where no station is reachable.
