- DTCoreText
- [iOS常用库汇总](http://www.jianshu.com/p/2ba717122951#%E5%AF%8C%E6%96%87%E6%9C%AC)
- [iOSLibraryCollections](https://github.com/mrhyh/iOS-LibraryCollections)

-
###2017-04-11
-xib中view点击事件，在一个有navigationController的viewcontroller中view加载自定义视图时会出现子视图内容向下位移20px的情况，另外加载自定义xib视图会出现xib子视图事件无法响应的情况；此种情况可以为viewcontroller加一个contentView，在这个子contentView中不会出现内容下移和事件无法响应的情况

-

###2017-05-23
1. 八大排序，三大查找 
	
	-冒泡排序（升序）
	1.从左到右相邻比较，大的右移。两层循环实现
	2.
	
	```
	void bubble_sort(vector<int> &nums)
	{
		for (int i = 0; i < nums.size()-1; i++) //n-1 time
		{
			for (int j = 0; j < nums.size()-i-1; j++)//n-i position
			{
				if (nums[j] > nums[j+1])
				{
					nums[j] += nums[j+1];
					nums[j+1] = nums[j] - nums[j+1];
					nums[j] -= nums[j+1];
				}
			}
		}
	}
	执行步数：（1+n）*n／2，==》时间复杂度：O(n^2)，空间复杂度：	O(n)
	```
	
	-插入排序(升序序)，
	
	1.从左开始，选出当前位置x，x与x前的数（y）进行比较，x<y,则交换。比较前i个数
	
	```
	void insert_sort(vector<int> &nums)
	{
		for (int i = 1; i < nums.size(); i++)//n-1 position
		{
			for (int j = i; j > 0; j--)//i time
			{
				if (nums[j] < nums[j-1])
				{
					nums[j-1] += nums[j];
					nums[j] = nums[j-1] - nums[j];
					nums[j-1] -= nums[j];
				}
			}
		}
	}
	时间复杂度：O(n^2) 空间复杂度:O(n)
	```
	
	-选择排序 （升序）
	选出最大（小）值放在头部
	
	```
	void selection_sort(vector<int> &nums)
	{
		for (int i = 0; i <num.size(); i++)//n position
		{
			int min = i;
			for (int j = i + 1; j<nums.size(); j++)//n-i time
			{
				if (nums[j] < nums[min])
				{
					min = j;
				}
			}
			nums[min] = nums[min] + nums[i];
			nums[i] = nums[min] - nums[i];
			nums[min] -= nums[i];
		}
	}
	```
	-希尔排序
	
	```
	void shell_sort(vector<int> $nums)
	{
		for (int gap = nums.size() >> 1; gap > 0; gap >>= 1)
		{
			for (int i = gap; i < nums.size(); i++)
			{
				int temp = nums[i];
				
				int j = i - gap;
				for(; j >= 0 && nums[j] > temp; j -= gap)
				{
					nums[j+gap] = nums[j];
				}
				nums[j + gap] = temp;
			}
		}
	}
	```
	-归并排序
	
	```
	void merge_array(vector<int> &nums, int b, int m, int e, vector<int> &temp)
	{
		int lb = b, rb = m, tb = b;
		while(lb != m && rb != e)
		{
			if (nums[lb] < nums[lb++])
			{
				temp[tb++] = nums[lb++];
			}else{
				temp[tb++] = nums[rb++];
			}
		}
		
		while (lb < m)
		{
			temp[tb++] = nums[lb++];
		}
		
		while (rb < e )
		{
			temp[tb++] = nums[rb++];
		}
		for (int i = b; i < e; i++)
		{
			nums[i] = temp[i];
		}
	}
	
	void merge_sort(vector<int> &nums, int b, int e, vector<int> &temp)
	{
		int m = (b + e) / 2;
		if (m != b )
		{
			merge_sort(nums, b, m, temp);
			merge_sort(nums, m, e, temp);
			merge_array(nums, b, m, temp);
		}
	}
	
	时间复杂度：O(nlogn) 空间复杂度：O(n)
	
	```
	-快速排序
	
	```
	void quick_sort(vector<int> &nums, int b, int e, vector<int> &temp)
	{
		int m = (b+e)/2;
		if (m != b)
		{
			int lb = b, rb = e-1;
			for (int i = b; i<e; i++)
			{
				if (i == m){
					continue;
				}
				if (nums[i] < nums[m])
				{
					temp[lb++] = nums[i];
				}else{
					temp[rb--] = nums[i];
				}
			}
			temp[lb] = nums[m];
			for (int i = b; i< e; i++)
			{
				nums[i] = temp[i];
			}
			
			quick_sort(nums, b, lb, temp);
			quick_sort(nums, lb + 1, e, temp);
		}
	}
	```
	-堆排序
	
	-基数排序
	
	```
	//获取最大位数
	void maxbit(vector<int> &nums)
	{
		int maxData = nums[0];
		
		for (int i = 1; i <nums.size(); i ++)
		{
			if (maxData < data[i])
			{
				maxData = data[i];
			}
		}
		int d = 1;
		while (maxData >= 10)
		{
			maxData /= 10;
			++d;
		}
		return d;
	}
	
	void radio_sort(vector<int> &nums)
	{
		int d = maxbit(nums);
		int size = nums.size();
		
		int *tmp = new int[size];
		int *count = new int[10];
		
		int i,j,k;
		int radix = 1;
		
		for(i = 1; i <= d; i++)
		{
			for(j=0; j < 10; i++){
				count[j] = 0;
			}
			for(j = 0; j < n; j++)
			{
				k = (nums[j] / radix) % 10;
				count[k] ++;
			}
			for(j = 1; j < 10; j ++)
			{
				count[j] = count[j - 1] + count[j];
			}
			for(j = n-1; j >= 0; j--)
			{
				k = (nums[j] / radix) % 10;
				tmp[count[k] - 1] = nums[j];
				count[k]--;
			}
			for(j = 0; j < n; j ++ )
			{
				nums[j] = tmp[j];
			}
			radix = radix * 10;
		}
		
		delete []tmp;
		delete []count;
	}
	```
	
	-1.顺序查找
	
	-2.二分查找
	
	-3.分块查找
	
	-4.散列表
	
2. 常见树的形式与树的增删查改 
	
	- 1.树的定义：一种抽象数据类型或是实作这种抽象数据类型的数据结构，用来模拟具有树状结构性质的数据集合。
	- 2.特点：
	
	 		1.每个节点有零个或多个子节点；
	 		2.没有父节点的节点称为根节点；
	 		3.每个非根节点有且仅有一个父节点；
	 		4.除了根节点外，每个节点可以分为多个不相交的子树；
	
3. 图的遍历方式与最短路径算法 

-

[django学习地址](http://usyiyi.cn/translate/django_182/index.html)

[git-liaoxuefeng](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013743858312764dca7ad6d0754f76aa562e3789478044000)

##git版本管理命令
- 1. git add filename #(把文件提交到暂存区stage/index)
- 2. git commit filename -m 'modify record' #(提交到master区--分支)
- 3.  git status #查看修改内容
- 4. git diff filename #查看文件修改记录
- 5. git log/reflog #查看版本及修改记录
- 6. git reset --hard HEAD^ #回朔上个版本(HEAD是master指针）
- 7. git reset --hard version #指定到特地版本
- 8. git checkout -- file #从版本库切出指定文件
- 9. git rm file #删除文件
- 10. git remote add origin git@github.com:
- 11. git checkout -b newmastername #克隆切换新分支
- 12. git branch mastername git checkout mastername #等价于11条
- 13. git merge < name > #把name合并到当前分支上
- 14. git branch -d < name > #把name分支删除
- 15. git merge --no-ff -m "merge intro" < name > #--no-ff 表示禁用fast forward方式
- 16. git remote -v #查看远程库信息
- 17. git tag < name > [commit ID] #为指定版本添加标签，默认当前版本
- 18. git show < tagname > #显示指定版本信息
- 19. git tag -a < tagname > -m "tag info" [head ID] #