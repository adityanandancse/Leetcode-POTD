# LEETCODE
# PROBLEM OF THE DAY SOLUTIONS

# 10/11/2024
# Question no. 3097 (https://leetcode.com/problems/shortest-subarray-with-or-at-least-k-ii)
# Solution i C++

class Solution {

public:

    void update(int number, vector<int>& vec, int val){
    
        for (int i = 0; i < 32; i++) {
        
            if((number >> i) & 1){
            
                vec[i] += val;
                
            }
            
        }
        
    }
    
    int getDecimalFromBinary(vector<int>& vec) {
    
        int num = 0;
        

        for(int i = 0; i < 32; i++) {
        
            if (vec[i] > 0) {
            
                num |= (1 << i);
            }
            
        }
        return num;
    }

    int minimumSubarrayLength(vector<int>& nums, int k) {
        int n = nums.size();

        int result = INT_MAX;

        int i = 0; 
        int j = 0;

        vector <int> vec(32, 0);

        while(j < n) {
            update(nums[j], vec, 1);

            while(i <= j && getDecimalFromBinary(vec) >= k) {
                result = min(result, j-i+1);
                update(nums[i], vec, -1);
                i++;
            }
            j++;
        }
        return result == INT_MAX ? -1 : result;
    }
};

# 9/11/2024
# Question no. 3133 Minimum Array End (https://leetcode.com/problems/minimum-array-end/)
# Solution in Java

class Solution {
    public long minEnd(int n, int x) {
        int i = 0;
        long m = n;
        long res = x;
        m--;

        while (m > 0) {
            while (((1L << i) & res) != 0) {
                i++;
            }
            res |= ((m & 1) << i);
            i++;
            m >>= 1;
        }
        return res;
    }
}


# 8/11/2024
# Question no. 1829 (https://leetcode.com/problems/maximum-xor-for-each-query/description/)
# Solution in Java

class Solution {

    public int[] getMaximumXor(int[] nums, int maximumBit) {
    
        int xor = 0;
        
        for (int num : nums) {
        
            xor ^= num;
            
        }
        
        int biggestNum = (int) Math.pow(2,maximumBit) -1;
        
        int[] res = new int  [nums.length];
        
        for (int i = 0; i<nums.length; i++) {
        
            res [i] = xor ^ biggestNum;
            
            xor ^= nums[nums.length -i -1];
            
        }
        
        return res;
        
    }
    
}




# 7/11/2024
# Questtion no. 2275 (https://leetcode.com/problems/largest-combination-with-bitwise-and-greater-than-zero/)
# Solution in java

class Solution {
    public int largestCombination(int[] candidates) {
        int [] bitCounts = new int[32];
        for (int num : candidates) {
            int i = 0;
            while (num != 0){
            bitCounts[i] += num & 1;
            num >>= 1;
            i++;
        }
    }
    int res = 0;
    for (int num : bitCounts) {
        res = Math.max(res, num);
    }
    return res;
}
}


# 6/11/2024
# Question no. 3011 Find if array can be sorted (https://leetcode.com/problems/find-if-array-can-be-sorted/description/)
# Solution in C++

class Solution {

public:

    bool canSortArray(vector<int>& nums) {
    
        int n = nums.size();
        
        int prev_segment_max=INT_MIN;
        
        int curr_segment_max = nums[0];
        
        int curr_segment_min = nums[0];
        
        int set_bit_count = __builtin_popcount(nums[0]);
        
        int i = 1;
        
        while(i<n){
        
            while(i<n and __builtin_popcount(nums[i])==set_bit_count){
            
                curr_segment_max = max(curr_segment_max, nums[i]);
                
                curr_segment_min = min(curr_segment_min, nums[i]);
                
                i++;  
            }
            
            if(prev_segment_max > curr_segment_min){
            
                return false;
                
            }
                else if(i<n){
                
                    prev_segment_max = curr_segment_max;
                    
                    curr_segment_max = nums[i];
                    
                    curr_segment_min = nums[i];
                    
                    set_bit_count = __builtin_popcount(nums[i]);
                    
                }
                
        }
        
            return true;
            
    }
    
};


# 5/11/2024
# Question no. 2914 Minimum no. of changes to make binary string beautiful (https://leetcode.com/problems/minimum-number-of-changes-to-make-binary-string-beautiful/description/)
# Solution in Java

class Solution {

    public int minChanges(String s) {
    
        int res = 0;
        
        for (int i = 0; i < s.length(); i += 2){
        
            if (s.charAt(i) != s.charAt(i + 1)){
            
                res++;
                
            }
            
        }
        
        return res;
        
    }
    
}


# 4/11/2024
# Question no. 3163 String Compression III (https://leetcode.com/problems/string-compression-iii/)
# Solution in C++:

class Solution {
public:
    string compressedString(string word) {
        int n = word.size();
        string res = "";
    
    int i = 1;
    int start = 0;
    while (i<n) {
        while(i<n and word[i]==word[i-1] and (i-start)<10)
        i++;

        if((i-start)==10) i--;

        res.append(to_string(i-start));
        res.push_back(word[start]);

        start = i;
        i++;
    }
    if (start == n-1){
        res.append(to_string(i-start));
        res.push_back(word[start]);
    }
    return res;
}
};

# 3/11/2024
# Question no. 796 Rotate String (https://leetcode.com/problems/rotate-string/)
# Solution in Java:

class Solution {

    public boolean rotateString(String s, String goal) {
    
        return s.length() == goal.length() && (s + s).contains(goal);
        
        
    }
    
}


# 2/11/2024
# Question no. 2490 Circular Sentence  (https://leetcode.com/problems/circular-sentence/)
# Solution in C++:

class Solution {

public:

    bool isCircularSentence(string sentence) {
    
        if(sentence.back()!=sentence[0])
        
        return false;
        
        int n=sentence.size();
        
        int i=0;
        
        while(i<n){
        
            while(i<n and sentence[i]!=' ')
            
            i+=1;
            
            if(i<n and sentence[i-1]!=sentence[i+1])
            
            return false;
            
            i+=1;
        }
        return true;
        
    }
    
};
