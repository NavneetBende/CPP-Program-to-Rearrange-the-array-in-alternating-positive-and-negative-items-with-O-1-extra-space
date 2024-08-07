Rearrange the Array in C++
 

Here, in this page we will discuss the program to Rearrange the Array in C++ . Rearrange in the way of alternating positive and negative items. Here, we will also discuss the efficient way of solving this problem in O(1) extra space. We are given with  an array of positive and negative numbers, we have to arrange them.
Number of positive and negative numbers need not be equal. If there are more positive numbers they appear at the end of the array. If there are more negative numbers, they too appear in the end of the array.

Rearrange the array in C++
Let’s discuss the brute force approach to solve this problem. As, here we need to maintain the order of the array and also solve this problem in O(1) extra space means without using extra space.

Method 1 – Brute force approach
Take the size of the array from the user and store it in variable say n.
Now, declare an array of n size and named it let say arr[], take n integer value from the user and store them in the created array.
Now, we will rearrange the array by using the following approach :
Iterate array from left to right i.e, 0 to n-1 index value. While iterating, find the first out of place element in the remaining unprocessed array.
An element is out of place if it is negative and at odd index, or it is positive and at even index.
Once we get an out of place element, we find the first element after it with opposite sign.
Then, We right rotate the sub-array between these two elements (including these two).
Now, the above approach takes O(N^2) time and O(1) space to solve the problem. In the second method we will discuss an efficient way to solve this problem.

Rearrange the array in C++
Code to rearrange the array in C++
#include <bits/stdc++.h>
using namespace std;

// Utility function to right rotate all elements between
// [outofplace, cur]
void rightrotate(int arr[], int n, int outofplace, int cur)
{
   char tmp = arr[cur];
   for (int i = cur; i > outofplace; i--)
      arr[i] = arr[i - 1];
   arr[outofplace] = tmp;
}

void rearrange(int arr[], int n)
{
   int outofplace = -1;

   for (int index = 0; index < n; index++)
   {
      if (outofplace >= 0)
      {
         if (((arr[index] >= 0) && (arr[outofplace] < 0))|| ((arr[index] < 0)&& (arr[outofplace] >= 0)))
         {
           rightrotate(arr, n, outofplace, index);

           // the new out-of-place entry is now 2 steps ahead
           if (index - outofplace >= 2)
             outofplace = outofplace + 2;
           else
             outofplace = -1;
         }
      }

     // if no entry has been flagged out-of-place
     if (outofplace == -1) {
         // check if current entry is out-of-place
         if (((arr[index] >= 0) && (!(index & 0x01)))|| ((arr[index] < 0) && (index & 0x01))) {
          outofplace = index;
     }
   }
 }
}

// A utility function to print an array 'arr[]' of size 'n'
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
      cout<<arr[i];
    cout<<endl;
}

// Driver code
int main()
{

   int n;
   cin>>n;

   int arr[n];
   for(int i=0; i<n; i++)
     cin>>arr[i];

   cout<<"Given array is \n";
   printArray(arr, n);

   rearrange(arr, n);

   cout<<"Rearranged array is \n";
   printArray(arr, n);

   return 0;
}
Input :

5 

-1 -2 8 9 -3

Output :

Given array is 

-1 -2 8 9 -3

Rearranged array is

-1 8 -2 9 -3

Related Pages
Given an array which consists of only 0, 1 and 2

Move all the negative elements to one side of the array

Minimum no. of Jumps to reach the end of an array 

Find Largest sum contiguous Subarray

Minimize the maximum difference between heights 

Method 2 – Efficient Algorithm
Sort the array in non-increasing order. Then we will count the number of positive and negative integers and store them in variables.
Then we will swap the one negative and one positive number in the odd positions till we reach our condition.
This will rearrange the array elements because we are sorting the array and accessing the element from left to right according to our need
 
Time And Space Complexity :
Time – Complexity: O(NlogN)
Space-complexity : O(1)
Code to rearrange the array in C++ :
#include <bits/stdc++.h>
using namespace std;

void fill1(int a[], int neg, int pos)
{
   if (neg % 2 == 1)
   {
     for(int i = 1; i < neg; i += 2)
     {
       int c = a[i];
       int d = a[i + neg];
       int temp = c;
       a[i] = d;
       a[i + neg] = temp;
     }
   }
   else
   {
      for(int i = 1; i <= neg; i += 2)
      {
        int c = a[i];
        int d = a[i + neg - 1];
        int temp = c;
        a[i] = d;
        a[i + neg - 1] = temp;
      }
   }
}

void fill2(int a[], int neg, int pos)
{
   if (pos % 2 == 1)
   {
     for(int i = 1; i < pos; i += 2)
     {
        int c = a[i];
        int d = a[i + pos];
        int temp = c;
        a[i] = d;
        a[i + pos] = temp;
     }
   }
   else
   {
      for(int i = 1; i <= pos; i += 2)
      {
         int c = a[i];
         int d = a[i + pos - 1];
         int temp = c;
         a[i] = d;
         a[i + pos - 1] = temp;
      }
   }
}



// A utility function to print an array 'arr[]' of size 'n'
void printArray(int arr[], int n)
{
   for (int i = 0; i < n; i++)
     cout<<arr[i]<<" ";
   cout<<"\n";
}

// Driver code
int main()
{

  int n;
  cin>>n;

  int arr[n];
  for(int i=0; i<n; i++)
    cin>>arr[i];

  cout<<"Given array is \n";
  printArray(arr, n);

  int neg = 0, pos = 0;
  for(int i = 0; i < n; i++)
  {
     if (arr[i] < 0)
     neg++;
     else
     pos++;
  }

  sort(arr, arr+n);
  printArray(arr, n);

  if (neg <= pos)
  {
    fill1(arr, neg, pos);
  }
  else
  {
     // Reverse the array in this condition
     int i, k, t;
     for(i = 0; i < n / 2; i++)
     {
        t = arr[i];
        arr[i] = arr[n - i - 1];
        arr[n - i - 1] = t;
     }
     fill2(arr, neg, pos);
   }
   cout<<"Rearranged array is \n";
   printArray(arr, n);
 
   return 0;
}
Input :

5 

9 -1 -9 4 -5


Output :

Given array is 

9 -1 -9 4 -5

Rearranged array is

9 -1 4 -5 -9
