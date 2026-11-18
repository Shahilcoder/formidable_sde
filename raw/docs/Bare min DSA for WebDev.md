# Bare min. DSA for WebDev

> *IMPORTANT
> 

# ***Arrays & Lists**

*Better to have it memorized all*

### **higher order functions:**

map, filter, reduce and all other existing instance methods in arrays

- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [https://lodash.com/docs/4.17.15](https://lodash.com/docs/4.17.15)

# ***Objects & Maps**

*Better to have it memorized all*

- declare
- Object.values
- delete obj[‘name’]
- caching concept
- [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)

```cpp
// taking array of objects and putting them inside map
// to access them in O(1)
// so you put O(n + m) efforts
// rather than using find() each time to get the object.
// O(n*m) effort

const map = {};

for (let obj of parents) {
	map[obj.id] = obj;
}

for (let pet of pets) {
	pet.parentName = map[pet.parentId].name;
}
```

# ***Sorting**

- just using the sorts
- sort() method of array

# ***Other Algos**

- Debouncing
- Memoization
- Cache invalidation; LRU (Least recently used)

# ***Stack & Queues**

Async processes/jobs uses **queue**, to push in events, and then the worker process dequeues and processes them, and flags it as done.

- throttling & debouncing
- memory stack & heap

# *Sets

- keep track of unique values
- `{1, 2, ‘b’}`

# **Trees**

- DOM
- DFS or BFS algos
- recursion

# **Graphs**

- Tree is a type of graph
- social media network, friendship graph
- A* algorithm
- recursion

# **Heaps & Priority Queues**

- list of people objects; someone got premium; put them at top of priority queue, so they get work done first.

# **Tries (prefix Tree)**

- for typeahead lookup
- autocompletes; search suggestions

# **Using a Debugger**

# **Use a Frame Graph**