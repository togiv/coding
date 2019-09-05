## <a href="http://acm.hdu.edu.cn/showproblem.php?pid=1229">还是A+B</a>

题目描述
> Problem Description
读入两个小于10000的正整数A和B，计算A+B。需要注意的是：如果A和B的末尾K（不超过8）位数字相同，请直接输出-1。
 

Input
> 测试输入包含若干测试用例，每个测试用例占一行，格式为"A B K"，相邻两数字有一个空格间隔。当A和B同时为0时输入结束，相应的结果不要输出。
 

Output
> 对每个测试用例输出1行，即A+B的值或者是-1。

Sample Input
1 2 1

11 21 1

108 8 2

36 64 3

0 0 1
 

Sample Output

3
-1
-1
100

注意必须是连续的相等，中间有一个不相等直接停止循环

代码：
```c++
#include<iostream>
using namespace std;
int equal(int s,int t){  //比较函数，相等返回1
	if (s==t){
		return 1;
	}else
	return 0;
}
int main(){
	int a,b,k,i,j;
	int sum;
	cin>>a>>b>>k;	
	while(!(a==0&&b==0)){
	i = a;
	j = b;
	sum = 0;
	if(i==j){  //若相等，直接输出
		cout<<-1<<endl;
		cin>>a>>b>>k;
		continue;
	}
	while(i>0||j>0){
		int temp = equal(i%10,j%10);
		if(temp){
			sum++;
		}else
			break; 有一个不相等直接停止循环
		i /= 10;
		j /= 10;
	}		
	if(sum>=k) //注意这里是>=
	cout<<-1<<endl;
	else
	cout<<a+b<<endl;
	cin>>a>>b>>k;
}
return 0;
}
```
