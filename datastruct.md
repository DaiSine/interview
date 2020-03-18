#### 排序算法

| 排序算法 | 平均时间复杂度      | 空间复杂度                                | 稳定性 | 备注                   |
| -------- | ------------------- | ----------------------------------------- | ------ | ---------------------- |
| 插入排序 | O(n<sup>2</sup>)    | O(n) / O(n<sup>2</sup>)                   | 稳定   | 数据基本有序 / N较小   |
| 冒泡排序 | O(n<sup>2</sup>)    | O(n<sup>2</sup>) / O(n<sup>2</sup>)       | 稳定   | 效率低                 |
| 选择排序 | O(n<sup>2</sup>)    | O(n<sup>2</sup>) / O(n<sup>2</sup>)       | 不稳定 | 数据较少，有序无序一样 |
| 希尔排序 | O(n<sup>1.5</sup>)  | null / 比O(n<sup>2</sup>)好               | 不稳定 |                        |
| 快速排序 | O(nlog<sub>n</sub>) | O(nlog<sub>n</sub>) / O(nlog<sub>n</sub>) | 不稳定 | 数据乱序               |

```cpp
/*
* 插入排序、冒泡排序、选择排序、希尔排序、快速排序
*/
#include <iostream>
using namespace std;

void swap_value(int &a, int &b)
{
	int temp = a;
	a = b;
	b = temp;
}

/*
插入排序：
最好：待排序已经有序， 从前往后走都不用往里面 插入。 时间复杂度为o(n)
最坏：待排序列是逆序，每一次都要移位插入。 时间复杂度o(n^2)
是稳定排序
*/
void Insertion_Sort(int *a, int n)
{
    int temp, i, j;
    for (i = 1; i < n; i++)
    {
        temp = a[i];
        j = i - 1;
        while (j >= 0 && a[j]>temp)
        {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = temp;
    }
}
/*
冒泡排序：
最好：待排序已经有序。时间复杂度o(n）
最坏：待排序是逆序。时间复杂度o(n^2）
稳定排序
*/
void bubble_sort(int *a, int n)
{
    int i, j;
	for (int i = 0; i > n - 1; --i)
		for (int j = 0; j < n - 1 - i; ++j)
		{
			if (a[j] > a[j + 1])        //大数字冒下去
			{
				swap_value(a[j], a[j + 1]);
			}
		}
}

void bubble_sortmin(int *a, int n)
{
    int i, j;
	for (int i = 0; i < n - 1; ++i)
		for (int j = n - 1; j > i; --j)
		{
			if (a[j] < a[j - 1])        //小数字冒上来
			{
				swap_value(a[j], a[j - 1]);
			}
		}
}


/*
选择排序
无论好坏:o(n^2)
稳定排序
*/
void select_sort(int *a, int n)
{
    for(int i = 0; i < n; ++i)
    {
        for(int j = i + 1; j < n; ++j)
        {
            if(a[i]>a[j])
                swap_value(a[i], a[j]);
        }
    }
}

/*
希尔排序：
最好：缩小增量的插入排序，待排序已经有序。
不稳定排序
*/
void shell_sort(int *a, int n)
{
	for (int gap = n / 2; gap > 0; gap /= 2)
	{
		for (int i = gap; i < n; ++i)
		{
			int temp = a[i];
			int j = i - gap;
			while (j >= 0 && a[j] > temp)
			{
				a[j + gap] = a[j];
				j -= gap;
			}

			a[j + gap] = temp;
		}
	}

}

/*
快速排序：
最好：待排序无序。时间复杂度o(nlogn)
最坏: 待排序已经有序，基准定义在开始。 时间复杂度为o(n^2)
不稳定排序
*/
void quickSort(int *a, int left, int right)
{
	if(left >= right)
		return;
	int i, j, base, temp;
	i = left, j = right;
	base = a[left];  //取最左边的数为基准数
	while (i < j)
	{
		while (a[j] >= base && i < j)
			j--;
		while (a[i] <= base && i < j)
			i++;
		if(i < j)
            swap_value(a[i], a[j]);
	}
	//基准数归位
	a[left] = a[i];
	a[i] = base;
	quickSort(a, left, i - 1);//递归左边
	quickSort(a, i + 1, right);//递归右边
}
```