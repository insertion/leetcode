#question
There are N gas stations along a circular route, where the amount of gas at station i is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.

Note:
The solution is guaranteed to be unique

#solution
```c
int canCompleteCircuit(int* gas, int gasSize, int* cost, int costSize) {
    int tank=0,total=0;
    int index=0;
    for (int i=0;i<gasSize;i++)
    {
        
         tank+=(gas[i]-cost[i]);
         if(tank<0)
         {
             total+=tank;
             tank=0;
             index=i+1;
         }
        
    }
    total+=tank;
    return total<0?-1:index;
}
```
#discussion
the answer is O(n)