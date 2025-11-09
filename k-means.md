https://youtu.be/ivFJZPYl2L0?si=T6F5v1k1N-6uQpvl
---

## 🧩 PROBLEM STATEMENT

> **Implement K-Means clustering/hierarchical clustering on sales_data_sample.csv dataset.
> Determine the number of clusters using the Elbow Method.**

### 🔍 What it means:

You are given a **sales dataset** (like total sales, quantity ordered, price, etc.).
You have to **group (cluster)** similar sales records together **without any predefined labels**.

For example:

* One group may contain **high-value orders**
* Another may have **medium orders**,
* Another may have **low orders**

This is an **unsupervised learning problem** — meaning **no right or wrong labels** are given.
We just find patterns automatically.

---

## 🧠 THEORY — What is K-Means Clustering?

K-Means is a **clustering algorithm** used to group data points into **K clusters**.

### ⚙️ How it works (step-by-step):

1. **Choose K** → number of clusters you want to make.
   Example: K = 3 (3 groups)

2. **Randomly place K points (centroids)** in your data.

3. **Assign each data point** to the nearest centroid → forms K groups.

4. **Move the centroids** to the average position of points in their group.

5. **Repeat** steps 3–4 until centroids stop moving (means stable clusters).

---

### 💡 The Elbow Method (to find K)

We don’t know how many clusters (K) to choose.
So, we try **different values of K (1, 2, 3, 4, 5...)**
and calculate **inertia (error)** — how tightly grouped points are in their cluster.

We plot K vs Inertia.
At first, inertia decreases fast, then slows down — like an arm bending at the **elbow** 🦾

The “bend point” shows the **best K**.

---

### 🧱 ASCII Diagram of Clustering

Here’s a simple imagination of clustering 👇

```
Before Clustering:
•  •   •       • •       • • •   •
(all data points are mixed)

After Clustering (K=3):
Cluster 1 → ○ ○ ○
Cluster 2 → ● ● ●
Cluster 3 → ▲ ▲ ▲
```

Each shape represents a different cluster found by the algorithm.

---

## 💻 CODE EXPLANATION

Let’s now understand the **code line-by-line** 👇

---

### Step 1️⃣ – Load the dataset

```python
data = pd.read_csv("sales_data_sample.csv", encoding='latin1')
```

* Reads the CSV file into a table (DataFrame).
* `encoding='latin1'` helps avoid character errors.

---

### Step 2️⃣ – Select numeric data

```python
num_data = data.select_dtypes(include=['float64', 'int64']).dropna()
```

* K-Means works only on **numbers** (not text).
* We select numeric columns like *SALES*, *QUANTITYORDERED*, *PRICEEACH*.

---

### Step 3️⃣ – Scale data

```python
scaler = StandardScaler()
scaled = scaler.fit_transform(num_data)
```

* Standardize data (make all columns have similar range).
* Example: SALES (in thousands) and QUANTITY (in tens) — scaling makes fair comparison.

---

### Step 4️⃣ – Elbow Method

```python
inertia = []
for k in range(1, 6):
    kmeans = KMeans(n_clusters=k, random_state=0)
    kmeans.fit(scaled)
    inertia.append(kmeans.inertia_)
```

* We try cluster counts K = 1, 2, 3, 4, 5
* `inertia_` = how spread out the points are inside clusters.
* We save these values to later plot the elbow curve.

---

### Step 5️⃣ – Plot the Elbow Curve

```python
plt.plot(range(1, 6), inertia, 'bo-')
plt.xlabel('Number of Clusters')
plt.ylabel('Inertia')
plt.title('Elbow Method')
plt.show()
```

* The plot helps visualize where the “bend” occurs → that’s your best K.

---

### Step 6️⃣ – Apply K-Means

```python
kmeans = KMeans(n_clusters=3, random_state=0)
data['Cluster'] = kmeans.fit_predict(scaled)
```

* We finally apply K-Means with chosen K (for example 3).
* It assigns each record to one cluster (0, 1, 2).

---

### Step 7️⃣ – Show results

```python
print(data[['SALES', 'QUANTITYORDERED', 'PRICEEACH', 'Cluster']].head())
```

* Prints the first few rows with the cluster number assigned.
* You can see which type of sales belong to which cluster.

---

## 🎯 Summary

| Step | Task                   | Purpose                         |
| ---- | ---------------------- | ------------------------------- |
| 1    | Load dataset           | Read sales data                 |
| 2    | Select numeric columns | K-Means works on numbers        |
| 3    | Scale data             | Equalize all feature ranges     |
| 4    | Elbow method           | Find best number of clusters    |
| 5    | Apply K-Means          | Group similar data              |
| 6    | Visualize              | Understand cluster distribution |

---

Would you like me to add a **tiny visual example** showing how “Elbow Method” curve looks (ASCII style)? It’ll make the concept stick in your head before viva.


### ✅ Final Easy Code (Google Colab Ready)

```python
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler

# Step 1: Load dataset
data = pd.read_csv("sales_data_sample.csv", encoding='latin1')

# Step 2: Select numeric columns
num_data = data.select_dtypes(include=['float64', 'int64']).dropna()

# Step 3: Scale data
scaler = StandardScaler()
scaled = scaler.fit_transform(num_data)

# Step 4: Elbow Method to find best k
inertia = []
for k in range(1, 6):
    kmeans = KMeans(n_clusters=k, random_state=0)
    kmeans.fit(scaled)
    inertia.append(kmeans.inertia_)

plt.plot(range(1, 6), inertia, 'bo-')
plt.xlabel('Number of Clusters')
plt.ylabel('Inertia')
plt.title('Elbow Method')
plt.show()

# Step 5: Apply KMeans with k=3 (example)
kmeans = KMeans(n_clusters=3, random_state=0)
data['Cluster'] = kmeans.fit_predict(scaled)

# Step 6: Show few results
print(data[['SALES', 'QUANTITYORDERED', 'PRICEEACH', 'Cluster']].head())
```

---

### 📘 Explanation (Short and Simple)

* We load the sales dataset
* Pick **only numeric columns** (like Sales, Quantity, Price)
* Normalize them (so large numbers don’t dominate)
* Use **Elbow Method** → a graph that helps find best number of clusters (where the curve bends)
* Apply **K-Means** with that `k` (for example, `k=3`)
* Add the cluster label to each record and print results

---

### 📊 Output (Example)

| SALES   | QUANTITYORDERED | PRICEEACH | Cluster |
| ------- | --------------- | --------- | ------- |
| 2871.00 | 30              | 95.70     | 0       |
| 2765.90 | 34              | 81.35     | 1       |
| 1456.50 | 10              | 145.65    | 2       |

---

