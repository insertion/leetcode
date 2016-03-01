#question
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Here are few examples.
[1,3,5,6], 5 → 2
[1,3,5,6], 2 → 1
[1,3,5,6], 7 → 4
[1,3,5,6], 0 → 0 


#solution1
```c
int searchInsert(int* nums, int numsSize, int target) {
    //nums  is a  sorted arrry 
    //numsSize is the size of array 
    //target is target
    int index=0;
    int left=0,right=numsSize-1;
    while(left<=right)
    {
        index=(left+right)/2;
        if(nums[index]<target)
            left=index+1;
        else if (nums[index]>target)
            right=index-1;
        else if (nums[index]==target)
            return index;
        
    }
    return left;
    
}
```
#solution2
```c
int searchInsert(int* nums, int numsSize, int target) {
    //nums  is a  sorted arrry 
    //numsSize is the size of array 
    //target is target
    int n=0;
    while(target>*nums)
        {
            nums++;
            n++;
            if(n>=numsSize)
            break;
        }
        return n;
    
}
```
#discussion
第一种：典型二分搜索，效率高

第二种：简单粗暴，效率低
```c
  class Solution {
    public:
        int searchInsert(vector<int>& nums, int target) {
            if(nums.size()==0)  return 0;
            int start=-1, end=nums.size();

            while(end-start>1){
                int mid=(start+end)/2;
                if(target <= nums[mid]) end=mid;
                else  start=mid;
            }
            return end;
        }
    };
```
起点逼近终点搜索法