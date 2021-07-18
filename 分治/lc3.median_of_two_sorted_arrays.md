


```java

class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int len = nums1.length + nums2.length;
        if (len % 2 == 1) {
            return findKth(nums1, 0, nums2, 0, len / 2 +1);
        } else {
            return (findKth(nums1, 0, nums2, 0, len / 2) + findKth(nums1, 0, nums2, 0, len / 2 + 1)) / 2.0;
        }
    }

    private int findKth(int[] A, int aStart, int[] B, int bStart, int k) {
        if (aStart >= A.length) {
            return B[bStart + k - 1];
        }
        if (bStart >= B.length) {
            return A[aStart + k - 1];
        }
        if (k == 1) {
            return Math.min(A[aStart], B[bStart]);
        }
        int aValue = aStart + k / 2 - 1 < A.length ? A[aStart + k / 2 - 1]  : Integer.MAX_VALUE;
        int bValue = bStart + k / 2 - 1 < B.length ? B[bStart + k / 2 - 1] : Integer.MAX_VALUE;
        if (aValue < bValue) {
            return findKth(A, aStart + k / 2, B, bStart, k - k / 2);
        }  else {
            return findKth(A, aStart, B, bStart + k / 2, k - k / 2);
        }                                        
                    
    }
}
```