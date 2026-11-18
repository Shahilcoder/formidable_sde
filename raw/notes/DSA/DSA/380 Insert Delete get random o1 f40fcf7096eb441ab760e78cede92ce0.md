# 380. Insert Delete get random o1

```cpp
class RandomizedSet {
private:
    unordered_map<int, int> mp;
    vector<int> nums;
public:
    RandomizedSet() {
    }
    
    bool insert(int val) {
        if (mp.find(val) != mp.end()) return false;
        nums.push_back(val);
        mp[val] = nums.size() - 1;
        
        return true;
    }

    bool remove(int val) {
        if (mp.find(val) == mp.end()) return false;
				
				// take the last element put into val's index in the array
				// pop the last part of array now
        int last = nums.back();
        nums[mp[val]] = last;
        nums.pop_back();

				// in the map also update that last's position is changed to val's index
        mp[last] = mp[val];
        // erase off the val key entry from the map
        mp.erase(val);

        return true;
    }
    
    int getRandom() {
        return nums[rand() % nums.size()];
    }
};
```