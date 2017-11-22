[一篇讲得很好的文章](https://gaohaoyang.github.io/2016/10/16/shuffle-algorithm/)

现代版本的描述与原始略有不同，因为如果按照原始方法，愚蠢的计算机会花很多无用的时间去计算上述第 3 步的剩余数字。这里的方法是在每次迭代时交换这个被取出的数字到原始列表的最后。这样就将时间复杂度从 O(n^2) 减小到了 O(n)。算法的伪代码如下：

```
-- To shuffle an array a of n elements (indices 0..n-1):
for i from n−1 downto 1 do
     j ← random integer such that 0 ≤ j ≤ i
     exchange a[j] and a[i]
```

```java
import java.util.Random;

public class FisherYatesShuffle {

	public static void main(String[] args) {
		int[] nums = new int[26];
		for(int i = 0; i < 26; i++)
			nums[i] = i;
		Random rand = new Random();
		shuffle(nums, rand);
		for(int num : nums)
			System.out.print(num + " ");
	}
	
	private static void shuffle(int[] nums, Random rand){
		for(int i = nums.length - 1; i >= 0; i--){
			int j = rand.nextInt(i + 1);
			swap(nums, i, j);
		}
	}
	
	private static void swap(int[] nums, int i, int j){
		int temp = nums[i];
		nums[i] = nums[j];
		nums[j] = temp;
	}
}
```
