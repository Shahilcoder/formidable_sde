# 771. Jewels and Stones

### ✅ **Approach 1: Using `unordered_set` (most common / cleanest)**

```cpp
int numJewelsInStones(string jewels, string stones) {
    unordered_set<char> jewelSet(jewels.begin(), jewels.end());
    int count = 0;
    for (char stone : stones)
        if (jewelSet.count(stone)) count++;
    return count;
}
```

**Time Complexity:**

- Building the set: `O(|J|)`
- Checking all stones: `O(|S|)` (amortized O(1) per lookup)
    
    → **Total: O(|J| + |S|)**
    

**Space Complexity:**

- `O(|J|)` for the set

✅ **Best trade-off** between simplicity, readability, and performance.

This is slightly more idiomatic than your `unordered_map` version.

---

### ⚙️ **Approach 2: Using `unordered_map` (My first approach)**

```cpp
int numJewelsInStones(string jewels, string stones) {
	unordered_map<char, int> jewelCountMap;
	int counter = 0;
	for (char jewel: jewels) jewelCountMap[jewel] = 0;
	
	for (char stone: stones) {
		if (jewelCountMap.find(stone) != jewelCountMap.end()) counter++;
	}
	
	return counter;
}
```

You’re creating a map with jewels as keys, and using it to check stones.

**Time Complexity:** `O(|J| + |S|)`

**Space Complexity:** `O(|J|)`

✅ Works fine, just a bit more memory overhead than `unordered_set` since you’re storing dummy values.

You don’t need counts here — a set is semantically cleaner.

---

### 🧮 **Approach 3: Brute Force (no extra data structure)**

```cpp
int numJewelsInStones(string jewels, string stones) {
    int count = 0;
    for (char stone : stones)
        for (char jewel : jewels)
            if (stone == jewel) count++;
    return count;
}
```

**Time Complexity:** `O(|J| * |S|)`

**Space Complexity:** `O(1)`

❌ **Inefficient**, but conceptually simplest — no extra memory.

---

### ⚡ **Approach 4: Using Boolean Array (if character set is small, e.g., ASCII)**

```cpp
int numJewelsInStones(string jewels, string stones) {
    vector<bool> isJewel(128, false);
    for (char jewel : jewels) isJewel[jewel] = true;

    int count = 0;
    for (char stone : stones)
        if (isJewel[stone]) count++;
    return count;
}
```

**Time Complexity:** `O(|J| + |S|)`

**Space Complexity:** `O(1)` (since the array size is constant 128 or 256)

✅ Fastest in practice (constant-time lookups, no hashing overhead).

💡 Great choice if you know input chars are ASCII (as in the LeetCode problem).