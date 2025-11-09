Here’s a **complete answer** with both **recursive** and **non-recursive (iterative)** Fibonacci programs in **C++**, along with their **time and space complexity analysis**.

---

## 🧮 Fibonacci Series Definition

The Fibonacci sequence is defined as:
[
F(n) = F(n-1) + F(n-2)
]
with base conditions:
[
F(0) = 0,; F(1) = 1
]

---

## ⚙️ 1. Non-Recursive (Iterative) Fibonacci Program

```cpp
#include <iostream>
using namespace std;

int fibonacci_iterative(int n) {
    if (n <= 1)
        return n;

    int prev2 = 0, prev1 = 1, current;
    for (int i = 2; i <= n; i++) {
        current = prev1 + prev2;
        prev2 = prev1;
        prev1 = current;
    }
    return current;
}

int main() {
    int n;
    cout << "Enter n: ";
    cin >> n;
    cout << "Fibonacci(" << n << ") = " << fibonacci_iterative(n) << endl;
    return 0;
}
```

### 🔍 **Time Complexity (Iterative):**

* Each Fibonacci number is computed once.
* The loop runs `n - 1` times.
  ✅ **O(n)**

### 💾 **Space Complexity (Iterative):**

* Uses only a few variables (`prev1`, `prev2`, `current`).
  ✅ **O(1)** (constant space)

---

## 🔁 2. Recursive Fibonacci Program

```cpp
#include <iostream>
using namespace std;

int fibonacci_recursive(int n) {
    if (n <= 1)
        return n;
    return fibonacci_recursive(n - 1) + fibonacci_recursive(n - 2);
}

int main() {
    int n;
    cout << "Enter n: ";
    cin >> n;
    cout << "Fibonacci(" << n << ") = " << fibonacci_recursive(n) << endl;
    return 0;
}
```

### 🔍 **Time Complexity (Recursive):**

Each call to `fibonacci_recursive(n)` makes **two recursive calls** except the base cases.
This forms an **exponential recursion tree**:

[
T(n) = T(n-1) + T(n-2) + O(1)
]

✅ **O(2^n)**

### 💾 **Space Complexity (Recursive):**

* At most `n` recursive calls are active in the call stack.
  ✅ **O(n)** (due to recursion depth)

---

## ⚖️ Summary Table

| Approach      | Time Complexity | Space Complexity | Remarks                 |
| ------------- | --------------- | ---------------- | ----------------------- |
| **Recursive** | O(2ⁿ)           | O(n)             | Simple but inefficient  |
| **Iterative** | O(n)            | O(1)             | Efficient and preferred |

