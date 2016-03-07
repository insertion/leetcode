# question
Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

For example,
Given nums = [1,3,-1,-3,5,3,6,7], and k = 3.

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7

Therefore, return the max sliding window as [3,3,5,5,6,7].

# solution
```c
/**
 * Return an array of size *returnSize.
 * Note: The returned array must be malloced, assume caller calls free().
 */
 #include<stdio.h>
 #include<stdlib.h>
int* maxSlidingWindow(int* nums, int numsSize, int k, int* returnSize) {
    int max=nums[0],index=0;
    int *ret;
    ret=(int *)malloc((numsSize-k+1)*sizeof(int));
    for(int i=0;i<numsSize-k+1;i++)
    {
       printf("%d-",index);
        if(index==i-1||i==0)
        {    
             max=nums[i];
             index=i;
             for(int j=i+1;j<i+k;j++)
            {
                if(max<nums[j])
                {
                max=nums[j];
                index=j;
                }
            }
        }
        else
        {
            if(max<nums[i+k-1])
                max=nums[i+k-1],
                index=i+k-1;
        }
        ret[i]=max;
    }
    *returnSize=numsSize-k+1;
    if(numsSize==0) *returnSize=0;
    return ret;
}
int main()
{
	int n[]={1,3,1,2,0,5};
//	printf("%d\n",sizeof(n)/4);
	int k;
	int *s=maxSlidingWindow(n,sizeof(n)/4,3,&k);
	int i;
	for(i=0;i<k;i++)
		printf("%d\n",*s++);
	return 0;
}
```