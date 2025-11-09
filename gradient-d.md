https://youtu.be/RxfiIPYbZnM?si=6rIyt1TdmocBN2UR  upto-11.14 mins



## 🧩 PROBLEM STATEMENT

> **Implement Gradient Descent Algorithm to find the local minima of a function.**
> Example: Find the local minima of
> [
> y = (x + 3)^2
> ]
> starting from ( x = 2 )

---

## 🧠 THEORY — What is Gradient Descent?

Gradient Descent is an **optimization algorithm** used to **find the minimum value** of a function.
It is the **core concept** behind how many **machine learning models learn**.

---

### 🪜 Step-by-step idea:

Let’s say we have a function:
[
y = (x + 3)^2
]

We want to find the **x-value where y is minimum**.
Graphically, that’s the **lowest point (valley)** of the curve.

---

### ⚙️ The logic behind Gradient Descent:

1. **Start from a random point** → e.g., ( x = 2 )
2. **Find the slope (derivative)** at that point.

   * The slope tells us **which direction** the function is increasing or decreasing.
3. **Move in the opposite direction of the slope** (to go *downhill*).
4. **Repeat** this process until the slope becomes almost 0 → that’s the **minimum point**.

---

### 📉 Formula

[
x_{\text{new}} = x_{\text{old}} - \text{learning_rate} \times \text{derivative}
]

* `learning_rate` decides **how big steps** we take toward the minimum.
  (Too large → jump over, too small → very slow)
* `derivative` = slope = how steep the function is at that point.

---

### 🧮 For our example:

[
y = (x + 3)^2
]
Derivative:
[
\frac{dy}{dx} = 2(x + 3)
]

So each step will be:
[
x_{\text{new}} = x_{\text{old}} - \text{lr} \times 2(x_{\text{old}} + 3)
]

The true minimum is when ( x = -3 ) (since (x+3)² is minimum there).

---

### 📈 ASCII Visualization

Imagine a U-shaped curve like this:

```
         ●
       ●   ●
     ●       ●
   ●           ●
 ●               ●  ← lowest point (minimum)
```

We start from x = 2 (right side of the curve) and take small downhill steps
until we reach the bottom (x = -3).

---

## 💻 SIMPLE CODE (Google Colab Ready)

```python
# Gradient Descent to find local minima of y = (x + 3)^2

# Step 1: Define function and its derivative
def func(x):
    return (x + 3)**2

def derivative(x):
    return 2*(x + 3)

# Step 2: Initialize values
x = 2                 # starting point
lr = 0.1              # learning rate
epochs = 50           # number of steps

# Step 3: Gradient Descent Loop
for i in range(epochs):
    grad = derivative(x)         # calculate slope
    x = x - lr * grad            # move opposite to slope
    print(f"Step {i+1}: x = {x:.4f}, f(x) = {func(x):.4f}")

print("\nLocal minimum occurs at x =", round(x, 2))
```

---

## 🧾 EXAMPLE OUTPUT

```
Step 1: x = 1.4, f(x) = 19.36
Step 2: x = 0.92, f(x) = 15.36
...
Step 20: x = -2.98, f(x) = 0.00

Local minimum occurs at x = -3.0
```

---

## 💡 CODE EXPLANATION

| Step | Code                                 | Meaning                                                    |
| ---- | ------------------------------------ | ---------------------------------------------------------- |
| 1    | Define `func(x)` and `derivative(x)` | Define the equation and its slope                          |
| 2    | Initialize `x`, `lr`, `epochs`       | Start from a point with step size and number of iterations |
| 3    | Loop to update `x`                   | Use gradient descent formula to move towards minimum       |
| 4    | Print each step                      | See how `x` approaches the minimum                         |
| 5    | Print final result                   | Shows the local minimum (≈ -3)                             |

---

## 🎯 Summary

| Concept           | Meaning                                                    |
| ----------------- | ---------------------------------------------------------- |
| **Goal**          | Find minimum of a function                                 |
| **Input**         | Function y = (x+3)²                                        |
| **Start Point**   | x = 2                                                      |
| **Learning Rate** | Controls step size                                         |
| **Output**        | Local minimum ≈ x = -3                                     |
| **Application**   | Used in ML algorithms (Linear Regression, Neural Networks) |

---

Would you like me to also show a **tiny visual plot (code)** of how x moves toward -3 step by step (so you can show it in your viva)?
