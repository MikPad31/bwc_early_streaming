# README_RF_PARAMS

## 🌲 `n_estimators`

**Definition:** Number of trees in the forest.
Each tree is trained on a bootstrap sample of the data and contributes one “vote.”

| When you increase it                                                                                                                                                                                    | When you decrease it                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| ✅ **Stability improves** — variance of the overall model decreases. Results become smoother and less sensitive to random seed.<br>⏱ **Slower training and prediction** (more trees to build and query). | ⚡ Faster training and prediction.<br>⚠️ Higher variance (more randomness) → performance can fluctuate more between runs. |

**Rule of thumb:** Keep increasing until out-of-bag error or CV score stabilizes. 200–500 is common; 1000+ rarely changes results much.

**default**: n_estimators=100

---

## 🌳 `max_depth`

**Definition:** The maximum depth each tree can grow.

| Increase `max_depth`                                                                                                    | Decrease `max_depth`                                                                                                  |
| ----------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| ✅ Trees grow deeper → can fit more complex patterns.<br>⚠️ **Higher variance** → risk of overfitting (memorizing noise). | ✅ Shallower trees → **more bias**, less variance.<br>Can underfit if too small (can’t capture complex relationships). |

**Typical tradeoff:** Deep trees capture rare interactions but risk overfitting small or noisy datasets. 8–20 is a common practical range.

**default**: max_depth=None

---

## 🌿 `min_samples_split`

**Definition:** Minimum number of samples required to split a node into child nodes.

| Increase `min_samples_split`                                                                                            | Decrease `min_samples_split`                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| ✅ Each node needs more data to split → trees become more **regularized** and smoother.<br>⚠️ Might miss subtle patterns. | ✅ Trees split more easily → more complex structure.<br>⚠️ Higher variance, can overfit small patterns or noise. |

**Typical values:** Between 2 and 10; higher for very noisy data or small sample sizes.

**default**: min_samples_split=2

---

## 🍃 `min_samples_leaf`

**Definition:** Minimum number of samples required in a leaf (final node).

| Increase `min_samples_leaf`                                                                             | Decrease `min_samples_leaf`                                                                   |
| ------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| ✅ Forces leaves to contain more samples → **smoother predictions**, less variance.<br>⚠️ Might underfit. | ✅ Leaves can represent smaller, sharper distinctions.<br>⚠️ Higher variance, overfitting risk. |

**Rule of thumb:**

* 1 = most flexible (default).
* 2–5 = safer for smaller or noisy datasets.
* 10+ = may be too coarse unless you have huge data.

**default**: min_samples_leaf=1

---

### 🧭 Putting it all together

| Parameter           | ↑ Increase →                   | ↓ Decrease →                |
| ------------------- | ------------------------------ | --------------------------- |
| `n_estimators`      | lower variance, higher compute | higher variance, faster     |
| `max_depth`         | lower bias, higher variance    | higher bias, lower variance |
| `min_samples_split` | higher bias, lower variance    | lower bias, higher variance |
| `min_samples_leaf`  | higher bias, lower variance    | lower bias, higher variance |

**Big picture:**

* To **regularize / prevent overfitting**, use shallower trees (`max_depth↓`), larger leaves (`min_samples_leaf↑`), or stricter splits (`min_samples_split↑`).
* To **capture complexity / reduce underfitting**, do the opposite.
* Always pair with **cross-validation** — the sweet spot is dataset-specific.

---
