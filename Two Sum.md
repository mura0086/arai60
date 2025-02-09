Step1
考えたこと
単純に全通り試してみることを考えるとO(N^2)と計算量が大きくなってしまう。
が、step1としてとりあえず書いてみることにした

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) 
    {
        int n = nums.size();
        for(int i = 0;i < n; i++)
        {
            for(int j= i + 1; j < n; j++)
            {
                if(i == j)
                    continue;
                if(nums[i] + nums[j] == target)
                {
                    return {i, j};
                }
            }
        }
        return {};     
    }
};
```

通った。よく見るとif(i==j)continue;は不要だった。

Step2
O(N)で解けないか考えたとき、mapに候補を入れながらtagetから候補を引いた値がmapに
存在するかどうかチェックしていけばよいのではないかと思った。

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) 
    {
        int n = nums.size();
        map<int, int> mp;
        for(int i = 0; i < n; i++)
        {
            auto tmp = mp.find(target - nums[i]);
            if(tmp != mp.end())
                return {i, tmp -> second};
            mp[nums[i]] = i; 
        }
        return {};
    }
};
```

通った。ほかの回答を参照した。
いずれの回答もmapを利用して同様の解き方をしているようだった
