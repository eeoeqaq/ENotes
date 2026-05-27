深度优先搜索


例一：将m分解为n个数的和
```
int m, arr[103]; // arr 用于记录方案 因为深度优先搜索，不用担心两次搜索在arr上互相影响
void dfs(int n, int i, int a) { 
	if (n == 0) { 
	for (int j = 1; j <= i - 1; ++j) 
	printf("%d ", arr[j]); 
	printf("\n"); 
	} 
	
		if (i <= m) {
	 for (int j = a; j <= n; ++j) {
	    arr[i] = j; 
	    dfs(n - j, i + 1, j); // 请仔细思考该行含义。
		}
	} 
 }
	  
// 主函数 
scanf("%d%d", &n, &m); 
dfs(n, 1, 1);
```

例二：P1706

例三：P1123
这里的dfs不明显。第一眼可能认为是某种贪心算法，但是每一步都会对之后的取数有影响，实在难以判断某种贪心算法的对错。
考虑到数据样本很小（观察到了），考虑搜索（没想到），![[206446b00ba3193c7f6d442b2cf3e52e.html]]