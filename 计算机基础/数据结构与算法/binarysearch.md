# 二分查找
## 二分查找的基本思想
	每次查找中间的元素，注意编程时，边界条件
## 时间复杂度
	O(log2n)
## 代码实现
`func BinarySearch(array []int, target int) (find bool, pos int){
	find = false
	pos = -1
	n := len(array)
	low := 0
	high := n - 1
	for low <= high {
		mid := (low + high) / 2;
		if array[mid] == target {
			find = true 
			pos = mid
			break
		} else if array[mid] < target {
			low = mid + 1
		} else {
			high = mid - 1
		}
	}
	return find, pos
}
`