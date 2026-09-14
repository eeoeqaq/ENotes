![[Pasted image 20260330082725.png]]


## 寄存器
以 `RAX` 为例（同一块硬件寄存器，不是四个不同寄存器）：
- `rax`：低 64 位（也就是整个 64 位）
- `eax`：低 32 位
- `ax`：低 16 位
- `al`：低 8 位
- `ah`：第 8~15 位（高 8 位，只在老式编码里常见）

## 常见指令
- movq 
- leaq
- addq等算术操作
![[Pasted image 20260330085601.png]]
`rdi rsi rdx rcx r8 r9`

## 条件码
example : f = a + b
CF(carry flag) : 进位借位标志
ZF(zero flag) : f == 0
OF(overflow flag) : t < 0
SF(signal flag) : (a > 0 && b > 0 && f < 0) || (a < 0 && b < 0 && f >= 0)
- 显式设置：
	- cmpq b a 执行a-b但不改变寄存器中的值
	- testq
- 读取：
	- setX
- 用于：
	- jX
## 分支语句与条件预测
![[Pasted image 20260330102813.png]]
cpu不喜欢这样无法预测的命令：**分支误预测惩罚**

介绍：条件传送
- cmovle          # if <=, result = eval

![[Pasted image 20260424162155.png]]

```c
void minmax1(long a[], long b[], long n) {
	for (i = 0; i < n; i++) { 
		if (a[i] > b[i]) { 
			long t = a[i]; a[i] = b[i]; b[i] = t; 
		} 
	}
} // bad


void minmax1(long a[], long b[], long n) {
	for (i = 0; i < n; i++) { 
		long max1 = a[i] > b[i] ? a[i] : b[i];
		long min1 = a[i] < b[i] ? a[i] : b[i];
		a[i] = min1;
		b[i] = max1;
	}
}
```
不适合的情况：
- 计算昂贵 `val = test(x) ? hard1(x) : hrad2(x)`
- 有副作用  `val = x>0 ? x*=7 : x+=3`
- 全部计算有风险 `val = p ? *p : 0`

