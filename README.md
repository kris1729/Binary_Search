# Binary_Search
### Search in Roted Sorted Array( Unique Element Only).

<Mathod-1> Use liner search and find the elemnet time complexity will be <O(n)>.

<Mathod-2> - in binary search if we divide into it two part , than it's fixed that <one of them
  will be always sorted >
than we check that in sorted part if element is present and find between in and leave unsorted part,
if in sorted part range if element is not , than we leave the sorted part and our seach space will be unsorted part.


```
int Search(vector<int> arr, int key, int size)
{
    int low = 0, heigh = size - 1;

    while (low <= heigh)
    {
        int mid = (low + heigh) / 2;

        if (arr[mid] == key)
            return mid;

        // left part is sorted

        if (arr[low] < arr[mid])
        {
            if (arr[low] <= key && key <= arr[heigh])
                heigh = mid - 1;
            else
                low = mid + 1;
        }

        // right part is sorted

        else
        {
            if (arr[mid] <= key && key <= arr[heigh])
                low = mid + 1;
            else
                heigh = mid - 1;
        }
    }
    return -1;
}


```

### Search in Roted Array (Not Unique Element)

- above mathod not work for the not unique element , because both  can be sorted 
- than we will add a extra condition <Trim> condition 

<if(arr[low]==arr[mid]&&arr[mid]==arr[heigh]) low++,heigh--,continue; >

```
  int Search(vector<int> arr, int key, int size)
{
    int low = 0, heigh = size - 1;

    while (low <= heigh)
    {
        int mid = (low + heigh) / 2;

        if (arr[mid] == key)
            return mid;

        // trim condition

        if (arr[low] == arr[mid] && arr[mid] == arr[heigh]){
            low++; heigh-- ; continue;}

        // left part is sorted

        if (arr[low] < arr[mid])
        {
            if (arr[low] <= key && key <= arr[heigh])
                heigh = mid - 1;
            else
                low = mid + 1;
        }

        // right part is sorted

        else
        {
            if (arr[mid] <= key && key <= arr[heigh])
                low = mid + 1;
            else
                heigh = mid - 1;
        }
    }
    return -1;
}


```

### Find Min in Roted Sorted Array(unique element)

<mathod-1> first sort all element and return first element<O(nlogn)>
<mathod-2> Linear search time Complexity will be <O(n)>
<mathod-3>Using Binary search
- divide array in two part one is left other is right 
- if left part is sorted than take arr[low] send for find in right part
 if right part is sorted than take arr[mid] and send for find in left part
- for more optimization if both part is soted than take arr[low] and break the loop

 ```
 
 int FindMin(vector<int> arr, int size)
{
    int low = 0, heigh = size - 1, mid, ans = INT_MAX;

    while (low <= heigh)
    {
        mid = (low + heigh) / 2;

        // both part sorted
        if (arr[low] <= arr[heigh])
        {
            ans = min(ans, arr[low]);
            break;
        }

        // left is sorted
        if (arr[low] <= arr[mid])
        {
            ans = min(ans, arr[low]);
            low = mid + 1;
        }

        // right part is sorted

        else
        {
            ans = min(ans, arr[mid]);
            heigh = mid - 1;
        }
    }
    return ans;
}

 ```