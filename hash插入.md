链接：https://ac.nowcoder.com/acm/contest/1080/B
来源：牛客网

题目描述 

> tokitsukaze有n个数，需要按顺序把他们插入哈希表中，哈希表的位置为0到n-1。
插入的规则是：
刚开始哈希表是空的。
对于一个数x，在哈希表中，如果(x mod n)的位置是空的，就把x放在(x mod n)的位置上。如果不是空的，就从(x mod n)往右开始找到第一个空的位置插入。若一直到n-1都不是空的，就从位置0开始继续往右找第一个空的位置插入。
因为哈希表总共有n个空位，需要插入n个数，所以每个数都能被插入。
现在tokitsukaze想知道把这n个数按顺序插入哈希表后，哈希表中的每个位置分别对应的是哪个数。

输入描述:

> 第一行包含一个正整数n(1≤n≤10^6)。
第二行包含n个非负整数x(0≤x≤10^9)，这些数按从左到右的顺序依次插入哈希表。

输出描述:

>输出一行，n个数，第i个数表示哈希表中位置为i所对应的数。(0≤i≤n-1)
示例1

输入

4
1 2 6 5

输出

5 1 2 6

说明

插入1时，1 mod 4=1，是空的，在位置1插入。
插入2时，2 mod 4=2，是空的，在位置2插入。
插入6时，6 mod 4=2，不是空的，找到下一个空的位置为3，所以在位置3插入。
插入5时，5 mod 4=1，不是空的，找到下一个空的位置为0，所以在位置0插入。

示例2

输入

4

3 0 7 11

输出

0 7 11 3

说明

插入3时，3 mod 4=3，是空的，在位置3插入。
插入0时，0 mod 4=0，是空的，在位置0插入。
插入7时，7 mod 4=3，不是空的，找到下一个空的位置为1，所以在位置1插入。
插入11时，11 mod 4=3，不是空的，找到下一个空的位置为2，所以在位置2插入。

用一个数组表示插入位置，如果插入位置已有数字则就一步一步往后走，如果数据量比较大，插入数据特殊，平移的代价非常大，最后会运行超时，如果该位置上的数字告诉我它后边有几个是有数字的，我直接跳过岂不是很好，想到并查集，刚开始数字增加一个属性`b`表示该插入到那个位置，一个位置插入数字之后，标志位马上和它后边的集合合并，合并到后边那个集合中，这样相连的集合就都会连在一起,下次再找该插入那个位置，直接找集合最后一个元素该插入的位置即可。
```c++
#include<iostream>
#include<string>
#include<vector>
using namespace std;
int father[1000001];
void init(int father[1000001]) {
    for (int i=0;i<1000001;i++){
        father[i]=i;
    }
}
int get(int x){
    if(father[x]==x)
        return x;
    return father[x]=get(father[x]);
}
void merge(int x, int y) {
    x = get(x);
    y = get(y);
    if (x != y) {
        father[x] = y;
    }
}
int main(){
    int n;
    cin>>n;  
    struct node{
        int a;
        int b;
    };
    node t[n];
    init(father);
    int b[n];
    for(int i=0;i<n;i++){
        cin>>t[i].a;
        t[i].b = t[i].a%n;
    }
    for(int j=0;j<n;j++){
        int index = get(t[j].b);
        b[index] = t[j].a;
        merge(index,index+1==n?0:index+1);
    }
    for(int j=0;j<n;j++){
        cout<<b[j]<<" ";
    }
}
```