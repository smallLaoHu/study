# 快速排序
## 快速排序的思想
	它的核心思想是:通过一趟排序将要排序的数列分成两个独立的新数列,其中一个新数列的每个元素都比另一个新数列的任何一个元素要小。之后,
	对这两个数列再次进行快速排序
## 算法性质
	1. 内部排序，即排序需要将元素加载到内存中去；
	2. 不稳定性，eg：2，2，1
	3. 时间复杂度 O(log2n)

## 代码实现
```
func QuickSort(array []int, low int, high int) {
	if low < high {
		pos := partition(array, low, high)
		QuickSort(array, low, pos - 1)
		QuickSort(array, pos + 1, high)
	}

}

func partition(array []int, low int, high int) int {
	var sentinel int = array[low]

	for low < high {
		for low < high && array[high] >= sentinel {
			high--
		}
		if low < high {
			array[low] = array[high]
			low = low + 1
		}
		for low < high && array[low] <= sentinel {
			low++
		}
		if low < high {
			array[high] = array[low]
			high = high - 1
		}
 	}
 	array[low] = sentinel
 	return low
}
```