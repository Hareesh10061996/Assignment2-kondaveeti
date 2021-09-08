# Assignment2-kondaveeti

# Hareesh Kondaveeti

###### Amarvathi - Guntur

I Love Amaravathi, India. I have lots of memories in my childhood.

**I Love Web Apps**

---
# Traveling from Maryville to Amarvathi Directions
    1.Take flight
      1.to Chicago
      2.to hyderabad
      3.Guntur
    2. Take cabs
      1.from Maryville to kansas airport ,
      2.From Hyderabad to Guntur.
    -Items to be brought for maximum enjoyment
      -Jacket
      -shoes
      -dresses
      -food.

https://github.com/Hareesh10061996/Assignment2-kondaveeti/blob/main/Aboutme.md

# Food items and drinks
Food items and drinks where can we get the items and who want to pay the bills for this items.

|Food/driknk |location | Amount shoulb be payed|
|------------|---------|-----------------------|
|Biryani     |Hyderabad| Rudra teja            |
|ICE cream   |Guntur   | Javeed                |
|Faluda      |Kukatpall| Manikanta             |
|Mandi       |Madhapur | Shiva krishna         |

# Pithy Quotes
> Opportunities don’t happen, you create them. *- Chris Grosser* <br>
> Start where you are. Use what you have. Do what you can. *- Arthur Ashe*

# Code Fencing

> Lowest Common Ancestor - O(N−−√) and O(logN) with O(N) preprocessing <br>


**[Lowest common Ancestor](https://cp-algorithms.com/graph/lca.html)**
```
struct LCA {
    vector<int> height, euler, first, segtree;
    vector<bool> visited;
    int n;

    LCA(vector<vector<int>> &adj, int root = 0) {
        n = adj.size();
        height.resize(n);
        first.resize(n);
        euler.reserve(n * 2);
        visited.assign(n, false);
        dfs(adj, root);
        int m = euler.size();
        segtree.resize(m * 4);
        build(1, 0, m - 1);
    }

    void dfs(vector<vector<int>> &adj, int node, int h = 0) {
        visited[node] = true;
        height[node] = h;
        first[node] = euler.size();
        euler.push_back(node);
        for (auto to : adj[node]) {
            if (!visited[to]) {
                dfs(adj, to, h + 1);
                euler.push_back(node);
            }
        }
    }

    void build(int node, int b, int e) {
        if (b == e) {
            segtree[node] = euler[b];
        } else {
            int mid = (b + e) / 2;
            build(node << 1, b, mid);
            build(node << 1 | 1, mid + 1, e);
            int l = segtree[node << 1], r = segtree[node << 1 | 1];
            segtree[node] = (height[l] < height[r]) ? l : r;
        }
    }

    int query(int node, int b, int e, int L, int R) {
        if (b > R || e < L)
            return -1;
        if (b >= L && e <= R)
            return segtree[node];
        int mid = (b + e) >> 1;

        int left = query(node << 1, b, mid, L, R);
        int right = query(node << 1 | 1, mid + 1, e, L, R);
        if (left == -1) return right;
        if (right == -1) return left;
        return height[left] < height[right] ? left : right;
    }

    int lca(int u, int v) {
        int left = first[u], right = first[v];
        if (left > right)
            swap(left, right);
        return query(1, 0, euler.size() - 1, left, right);
    }
};
```





