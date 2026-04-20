---
title: '2024程序设计天梯赛'
description: '个人训练以及题解...'
publishDate: '2026-04-13 21:08:01'
tags:
  - 算法
  - 天梯赛
heroImage: { src: './thumbnail.png', alt: 'an image targeting my article', color: '#7fa8de' }
---
### 前言
已经大半年没练过题了，马上就2026天梯赛了，加训中....
2024团体程序设计天梯赛，这是我大一的时候第一次参加天梯赛，当时只拿了155分，距离拿奖国三还差20分，对于当时来说拿奖挺难的。


### <span style="color:green">L1</span>

#### <span style="color:green">1-1~1-3</span>
ヽ (✿ﾟ▽ﾟ) ノ略略略

#### <span style="color:green">1-4 四项全能</span>
##### 题目描述
新浪微博上有一个帖子给出了一道题：全班有 50 人，有 30 人会游泳，有 35 人会篮球，有 42 人会唱歌，有 46 人会骑车，至少有（ ）人四项都会。
发帖人不会做这道题，但是回帖有会做的：每一个才艺是一个技能点，一共是 30 + 35 + 42 + 46 = 153 个技能点，50 个人假设平均分配，每人都会 3 个技能那也只有 150，所以至少有 3 人会四个技能。
本题就请你写个程序来自动解决这类问题：给定全班总人数为 n，其中有 m 项技能，分别有 k~1~、k~2~、……、k~m~个人会，问至少有多少人 m 项都会。

##### 输入格式:
输入在第一行中给出 2 个正整数：n（4≤n≤1000）和 m（1<m≤n/2），分别对应全班人数和技能总数。随后一行给出 m 个不超过 n 的正整数，其中第 i 个整数对应会第 i 项技能的人数。

##### 输出格式：
输出至少有多少人 m 项都会。

##### 输入样例:
```
50 4
30 35 42 46
```

##### 输出样例:
```
3
```

##### 思路
简单的数学题。如样例,可以贪心的想,$50$人中$30$人会k~1~,剩下$20$人会k~2~,那么必定有 $35-20=15$个人同时会这两项技能,同理，
剩下$50-15=35$个人会k~3~,那么只有$42-35=7$人同时掌握三项技能。


##### 个人参考代码
```c++
#include<bits/stdc++.h>
#include<unordered_map>
using namespace std;
#define int long long
#define endl "\n"
void solve() {
	int n, m;
	cin >> n >> m;
	int ans = n;
	for (int i = 1; i <= m; i++) {
		int x;
		cin >> x;
		ans = ans - (n - x);
	}
	cout << max(ans, int(0));
}
signed main() {
	ios_base::sync_with_stdio(false);
	cin.tie(0);
	cout.tie(0);
	int tt;
	tt = 1;
	while (tt--) {
		solve();
		if (tt != 0)cout << endl;
	}
	return 0;
}
```

#### <span style="color:green">1-5 别再来这么多猫娘了！</span>

##### 题目描述
你会得到一段由大小写字母、数字、空格及 ASCII 码范围内的标点符号的文字，以及若干个违禁词以及警告阈值，你需要首先检查内容里有多少违禁词，如果少于阈值个，则简单地将违禁词替换为<censored>；如果大于等于阈值个，则直接输出一段警告并输出有几个违禁词。

##### 输入格式:
输入第一行是一个正整数 N (1≤N≤100)，表示违禁词的数量。接下来的 N 行，每行一个长度不超过 10 的、只包含大小写字母、数字及 ASCII 码范围内的标点符号的单词，表示应当屏蔽的违禁词。
然后的一行是一个非负整数 k (0≤k≤100)，表示违禁词的阈值。
最后是一行不超过 5000 个字符的字符串，表示需要检查的文字。
从左到右处理文本，违禁词则按照输入顺序依次处理；对于有重叠的情况，无论计数还是替换，查找完成后从违禁词末尾继续处理。

##### 输出格式:
如果违禁词数量小于阈值，则输出替换后的文本；否则先输出一行一个数字，表示违禁词的数量，然后输出He Xie Ni Quan Jia!。

##### 输入样例:
```
5
MaoNiang
SeQing
BaoLi
WeiGui
BuHeShi
4
BianCheng MaoNiang ba! WeiGui De Hua Ye Keyi Shuo! BuYao BaoLi NeiRong.
```

##### 输出样例:
```
BianCheng <censored> ba! <censored> De Hua Ye Keyi Shuo! BuYao <censored> NeiRong.
```


##### 思路
放在前面已经是一道很难的字符串题了,两年前写的时候只拿了两三分...在替换字符串的过程中可能会导致无限替换下去。因此只需要先将违禁词替换成一个特定的东西，最后再全部替换回 "< censored > "即可

##### 个人参考代码
```c++
#include<bits/stdc++.h>
#include<unordered_map>
using namespace std;
#define int long long
#define endl "\n"
void solve() {
	int n;
	cin >> n;
	vector<string>sv;
	for (int i = 1; i <= n; i++) {
		string s;
		cin >> s;
		sv.push_back(s);
	}
	int maxk;
	cin >> maxk;
	string s;
	int now = 0;
	getchar();
	getline(cin, s);
	for (int j = 0; j < n; j++) {
		string ans;
		for (int i = 0; i < s.size(); i++) {
			int maxs = sv[j].size() - 1 + i;
			if (maxs >= s.size()) {
				for (int k = i; k < s.size(); k++)ans += s[k];
				break;
			}
			int flag = 1;
			for (int k = 0; k < sv[j].size(); k++) {
				if (s[i + k] != sv[j][k]) {
					flag = 0;
					break;
				}
			}
			if (flag) {
				ans += "****";
				i += sv[j].size() - 1;
				now++;
				continue;
			}
			ans += s[i];
		}
		s = ans;
	}
	while (s.find("****") != -1) {
		int pos = s.find("****");
		s = s.substr(0, pos) + "<censored>" + s.substr(pos + 4);
	}
	if (now >= maxk)cout <<now<<endl<< "He Xie Ni Quan Jia!";
	else cout << s;
}
signed main() {
	int tt;
	tt = 1;
	while (tt--) {
		solve();
	}
	return 0;
}
```

#### <span style="color:green">1-6 兰州牛肉面</span>
#### <span style="color:green">1-7 整数的持续性</span>
都是很简单的模拟题相比前一题简单太多了

#### <span style="color:green">1-8 九宫格</span>
##### 题目描述
九宫格是一款数字游戏，传说起源于河图洛书，现代数学中称之为三阶幻方。游戏规则是：将一个 9×9 的正方形区域划分为 9 个 3×3 的正方形宫位，要求 1 到 9 这九个数字中的每个数字在每一行、每一列、每个宫位中都只能出现一次。
本题并不要求你写程序解决这个问题，只是对每个填好数字的九宫格，判断其是否满足游戏规则的要求。

##### 输入格式：
输入首先在第一行给出一个正整数 n（≤10），随后给出 n 个填好数字的九宫格。每个九宫格分 9 行给出，每行给出 9 个数字，其间以空格分隔。

##### 输出格式：
对每个给定的九宫格，判断其中的数字是否满足游戏规则的要求。满足则在一行中输出 1，否则输出 0。

##### 输入样例：
```
3
5 1 9 2 8 3 4 6 7
7 2 8 9 6 4 3 5 1
3 4 6 5 7 1 9 2 8
8 9 2 1 4 5 7 3 6
4 7 3 6 2 8 1 9 5
6 5 1 7 3 9 2 8 4
9 3 4 8 1 6 5 7 2
1 6 7 3 5 2 8 4 9
2 8 5 4 9 7 6 1 3
8 2 5 4 9 7 1 3 6
7 9 6 5 1 3 8 2 4
3 4 1 6 8 2 7 9 5
6 8 4 2 7 1 3 5 9
9 1 2 8 3 5 6 4 7
5 3 7 9 6 4 2 1 8
2 7 9 1 5 8 4 6 3
4 5 8 3 2 6 9 7 1
1 6 3 7 4 9 5 8 3
81 2 5 4 9 7 1 3 6
7 9 6 5 1 3 8 2 4
3 4 1 6 8 2 7 9 5
6 8 4 2 7 1 3 5 9
9 1 2 8 3 5 6 4 7
5 3 7 9 6 4 2 1 8
2 7 9 1 5 8 4 6 3
4 5 8 3 2 6 9 7 1
1 6 3 7 4 9 5 8 2
```
##### 输出样例：
```
1
0
0
```
##### 思路
感觉是很好的一道模拟题，不会为了特意去麻烦而去麻烦
##### 个人参考代码
```c++
#include<bits/stdc++.h>
#include<unordered_map>
using namespace std;
#define int long long
#define endl "\n"
void solve() {
	vector<vector<int>> v(10,vector<int>(10));
	for (int i = 1; i <= 9; i++)
		for (int j = 1; j <= 9; j++) cin >> v[i][j];
	int flag = 1;
	set<int> s;
	for (int i = 1; i <= 9; i++) {
		s.clear();
		for (int j = 1; j <= 9; j++) {
			s.insert(v[i][j]);
		}
		if (s.size() != 9 || *s.begin() != 1 || *s.rbegin() != 9)flag = 0;
	}
	for (int i = 1; i <= 9; i++) {
		s.clear();
		for (int j = 1; j <= 9; j++) {
			s.insert(v[j][i]);
		}
		if (s.size() != 9 || *s.begin() != 1 || *s.rbegin() != 9)flag = 0;
	}
	for (int i = 1; i <= 9; i++) {
		s.clear();
		for (int j = 1; j <= 9; j++) {
			s.insert(v[(i-1)%3*3+1 + (j - 1) / 3][(j - 1) % 3 + 1+(i-1)/3*3]);
		}
		if (s.size() != 9 || *s.begin() != 1 || *s.rbegin() != 9)flag = 0;
	}
	if (flag)cout << 1;
	else cout << 0;
}
signed main() {
	int tt;
	tt = 1;
	cin >> tt;
	while (tt--) {
		solve();
		if (tt != 0)cout << endl;
	}
	return 0;
}
```
### <span style="color:wheat">L2</span>

#### <span style="color:wheat">2-1 鱼与熊掌</span>

##### 题目描述
《孟子 · 告子上》有名言：“鱼，我所欲也，熊掌，亦我所欲也；二者不可得兼，舍鱼而取熊掌者也。”但这世界上还是有一些人可以做到鱼与熊掌兼得的。
给定 n 个人对 m 种物品的拥有关系。对其中任意一对物品种类（例如“鱼与熊掌”），请你统计有多少人能够兼得？

##### 输入格式：
输入首先在第一行给出 2 个正整数，分别是：n（≤10^5^）为总人数（所有人从 1 到 n 编号）、m（2≤m≤10^5^）为物品种类的总数（所有物品种类从 1 到 m 编号）。随后 n 行，第 i 行（1≤i≤n）给出编号为 i 的人所拥有的物品种类清单，格式为：
```
K M[1] M[2] ... M[K]
```
其中 K（≤10^3^）是该人拥有的物品种类数量，后面的 M[*] 是物品种类的编号。题目保证每个人的物品种类清单中都没有重复给出的种类。
最后是查询信息：首先在一行中给出查询总量 Q（≤100），随后 Q 行，每行给出一对物品种类编号，其间以空格分隔。题目保证物品种类编号都是合法存在的。

##### 输出格式：
对每一次查询，在一行中输出两种物品兼得的人数。

##### 输入样例：
```
4 8
3 4 1 8
4 7 1 8 4
5 6 5 1 2 3
4 3 2 4 8
3
2 3
7 6
8 4
```
##### 输出样例：
```
2
0
3
```
##### 思路
用map存，物品对应人，查询时再用一个新的map查看两者兼有的人数。
（注:用unordered_map,map会超时）
##### 个人参考代码
```c++
#include<bits/stdc++.h>
#include<unordered_map>
using namespace std;
#define int long long
#define endl "\n"
void solve() {
	int n,m;
	cin >> n>>m;
	unordered_map<int, vector<int>> mp;
	for (int i = 1; i <= n; i++) {
		int k;
		cin >> k;
		for (int j = 1; j <= k; j++) {
			int x;
			cin >> x;
			mp[x].push_back(i);
		}
	}
	int q;
	cin >> q;
	vector<int> ans;
	while (q--) {
		int x, y;
		cin >> x >> y;
		map<int, int>mp2;
		int tans = 0;
		for (int i = 0; i < mp[x].size(); i++) {
			mp2[mp[x][i]]++;
		}
		for (int i = 0; i < mp[y].size(); i++) {
			if (mp2[mp[y][i]] == 1) {
				tans++;
			}
		}
		ans.push_back(tans);
	}
	for (int i = 0; i < ans.size(); i++) {
		cout << ans[i];
		if (i != ans.size() - 1)cout << endl;
	}
}
signed main() {
	ios_base::sync_with_stdio(false);
	cin.tie(0);
	cout.tie(0);
	int tt;
	tt = 1;
	while (tt--) {
		solve();
		if (tt != 0)cout << endl;
	}
	return 0;
}
```

#### <span style="color:wheat">2-2 懂蛇语</span>

##### 题目描述
在《一年一度喜剧大赛》第二季中有一部作品叫《警察和我之蛇我其谁》，其中“毒蛇帮”内部用了一种加密语言，称为“蛇语”。蛇语的规则是，在说一句话 A 时，首先提取 A 的每个字的首字母，然后把整句话替换为另一句话 B，B 中每个字的首字母与 A 中提取出的字母依次相同。例如二当家说“九点下班哈”，对应首字母缩写是 JDXBH，他们解释为实际想说的是“京东新百货”……
本题就请你写一个蛇语的自动翻译工具，将输入的蛇语转换为实际要表达的句子。

##### 输入格式：
输入第一行给出一个正整数 N（≤10^5^），为蛇语词典中句子的个数。随后 N 行，每行用汉语拼音给出一句话。每句话由小写英文字母和空格组成，每个字的拼音由不超过 6 个小写英文字母组成，两个字的拼音之间用空格分隔。题目保证每句话总长度不超过 50 个字符，用回车结尾。注意：回车不算句中字符。
随后在一行中给出一个正整数 M（≤10^3^），为查询次数。后面跟 M 行，每行用汉语拼音给出需要查询的一句话，格式同上。

##### 输出格式：
对每一句查询，在一行中输出其对应的句子。如果句子不唯一，则按整句的字母序输出，句子间用 | 分隔。如果查不到，则将输入的句子原样输出。
注意：输出句子时，必须保持句中所有字符不变，包括空格。

##### 输入样例：
```
8
yong yuan de shen
yong yuan de she
jing dong xin bai huo
she yu wo ye hui shuo yi dian dian
liang wei bu yao chong dong
yi  dian dian
ni hui shuo she yu a
yong yuan de sha
7
jiu dian xia ban ha
shao ye wu ya he shui you dian duo
liu wan bu yao ci dao
ni hai shi su yan a
yao diao deng
sha ye ting bu jian
y y d s
```

##### 输出样例：
```
jing dong xin bai huo
she yu wo ye hui shuo yi dian dian
liang wei bu yao chong dong
ni hui shuo she yu a
yi  dian dian
sha ye ting bu jian
yong yuan de sha|yong yuan de she|yong yuan de shen
```

##### 思路
字符串操作题，用map存，首字母组成的字符串对应内容，需要嵌套vector容器并排序。需要注意，有空格的出现时机以及数量（空格会连续出现）。

##### 个人参考代码
```c++
#include<bits/stdc++.h>
#include<unordered_map>
using namespace std;
#define int long long
#define endl "\n"
void solve() {
	int n;
	cin >> n;
	getchar();
	map<string, vector<string>>mp;
	for (int i = 1; i <= n; i++) {
		string s;
		getline(cin, s);
		string ts;
		if(s[0]!=' ')ts += s[0];
		for (int i = 0; i < s.size()-1; i++) {
			if (s[i] == ' ' && s[i + 1] != ' ')ts += s[i + 1];
		}
		mp[ts].push_back(s);
	}
	int m;
	cin >> m;
	vector<string> ans;
	for (auto& it : mp) {
		sort(it.second.begin(), it.second.end(), [](string& a, string& b) {
			return a < b;
			});
	}
	getchar();
	for (int i = 1; i <= m; i++) {
		string s;
		getline(cin, s);
		string ts;
		if (s[0] != ' ')ts += s[0];
		for (int i = 0; i < s.size()-1; i++) {
			if (s[i] == ' ' && s[i + 1] != ' ')ts += s[i + 1];
		}
		string ts2;
		if (!mp[ts].empty()) {
			for (int j = 0; j < mp[ts].size(); j++) {
				ts2 += mp[ts][j];
				if (j != mp[ts].size() - 1)ts2 += '|';
			}
		}
		else ts2 = s;
		ans.push_back(ts2);
	}
	for (int i = 0; i < ans.size(); i++) {
		cout << ans[i];
		if (i != ans.size() - 1)cout << endl;
	}
}
signed main() {
	int tt;
	tt = 1;
	while (tt--) {
		solve();
		if (tt != 0)cout << endl;
	}
	return 0;
}
```

#### <span style="color:wheat">2-3 满树的遍历</span>

##### 题目描述
一棵“k 阶满树”是指树中所有非叶结点的度都是 k 的树。给定一棵树，你需要判断其是否为 k 阶满树，并输出其前序遍历序列。

注：树中结点的度是其拥有的子树的个数，而树的度是树内各结点的度的最大值。

##### 输入格式：
输入首先在第一行给出一个正整数 n（≤10^5^），是树中结点的个数。于是设所有结点从 1 到 n 编号。
随后 n 行，第 i 行（1≤i≤n）给出第 i 个结点的父结点编号。根结点没有父结点，则对应的父结点编号为 0。题目保证给出的是一棵合法多叉树，只有唯一根结点。

##### 输出格式：
首先在一行中输出该树的度。如果输入的树是 k 阶满树，则加 1 个空格后输出 yes，否则输出 no。最后在第二行输出该树的前序遍历序列，数字间以 1 个空格分隔，行首尾不得有多余空格。
注意：兄弟结点按编号升序访问。

##### 输入样例 1：
```
7
6
5
5
6
6
0
5
```

##### 输出样例 1：
```
3 yes
6 1 4 5 2 3 7
```

##### 思路
判断树的度（除零外）必须相同，用二维数组存边，然后对点排序，最后是经典的**深度优先搜索**。
##### 个人参考代码
```c++
#include<bits/stdc++.h>
#include<unordered_map>
using namespace std;
#define int long long
#define endl "\n"
void solve() {
	int n;
	cin >> n;
	int g;
	vector<vector<int>> v(n + 1);
	for (int i = 1; i <= n; i++) {
		int x;
		cin >> x;
		if (x == 0) g = i;
		else v[x].push_back(i);                                      
	}
	int flag = 1;
	map<int, int>mp;
	int ans = 0;
	vector<int> qianxv;
	for (int i = 1; i <= n; i++) {
		if (v[i].size() != 0) { 
			mp[v[i].size()]++;
		}
		ans = max(ans, (int)v[i].size());
	}
	if (mp.size() > 1)flag = 0;
	auto dfs = [&](auto&&self,int i)->void{
		qianxv.push_back(i);
		sort(v[i].begin(),v[i].end());
		for (int j = 0; j < v[i].size(); j++) {
			self(self,v[i][j]);
		}
	};
	dfs(dfs,g);
	cout << ans << " ";
	if (flag)cout << "yes";
	else cout << "no";
	cout << endl;
	for (int i = 0; i < qianxv.size(); i++)
	{
		cout << qianxv[i];
		if (i != n - 1)cout << " ";
	}
}
signed main() {
	ios_base::sync_with_stdio(false);
	cin.tie(0);
	cout.tie(0);
	int tt;
	tt = 1;
	while (tt--) {
		solve();
		if (tt != 0)cout << endl;
	}
	return 0;
}
```

#### <span style="color:wheat">2-4 吉利矩阵</span>

##### 题目描述
所有元素为非负整数，且各行各列的元素和都等于 7 的 3×3 方阵称为“吉利矩阵”，因为这样的矩阵一共有 666 种。
本题就请你统计一下，把 7 换成任何一个 [2,9] 区间内的正整数 L，把矩阵阶数换成任何一个 [2,4] 区间内的正整数 N，满足条件“所有元素为非负整数，且各行各列的元素和都等于 L”的 N×N 方阵一共有多少种？

##### 输入格式：
输入在一行中给出 2 个正整数 L 和 N，意义如题面所述。数字间以空格分隔。

##### 输出格式：
在一行中输出满足题目要求条件的方阵的个数。

##### 输入样例：
```
7 3
```
##### 输出样例：
```
666
```

##### 思路
当年在比赛时看到这题真的吓到了，以为是很难的数学结论...前几天模拟赛的时候再看，原来是暴力搜索，但因为题目取值范围看错导致依旧拿零蛋。这题**暴力搜索+剪枝**即可通过。
##### 个人参考代码
```c++
#include<bits/stdc++.h>
#include<unordered_map>
using namespace std;
#define int long long
#define endl "\n"
int ans = 0;
vector<vector<int>> v(100, vector<int>(100));
void dfs(int m, int n, int x, int y) {
	int maxk = m;
	int limy = 0,limx=0;
	for (int i = 1; i < y; i++) limx+=v[x][i];
	for (int i = 1; i < x; i++)limy+=v[i][y];
	if (y == n&&x!=n) {
		if (limy + m - limx > m)return;
		v[x][y] = m - limx;
		dfs(m, n, x + 1, 1);
		return;
	}
	if (x == n && y != n) {
		if (limx + m - limy > m)return;
		v[x][y] = m - limy;
		dfs(m, n, x, y+1);
		return;
	}
	if (x == n && y == n) {
		if (limy == limx) { 
			ans++;
		}
		return;
	}
	maxk -=max(limx, limy);
	for (int i = 0; i <= maxk; i++) {
		v[x][y] = i;
		dfs(m, n, x, y + 1);
	}
}
void solve() {
	int m, n;
	cin >> m >> n;
	dfs(m, n, 1, 1);
	cout << ans;
}
signed main() {
	ios_base::sync_with_stdio(false);
	cin.tie(0);
	cout.tie(0);
	int tt;
	tt = 1;
	while (tt--) {
		solve();
		if (tt != 0)cout << endl;
	}
	return 0;
}
```

### <span style="color:red">L3</span>
#### <span style="color:red">3-1 夺宝大赛</span>
##### 题目描述
夺宝大赛的地图是一个由 n×m 个方格子组成的长方形，主办方在地图上标明了所有障碍、以及大本营宝藏的位置。参赛的队伍一开始被随机投放在地图的各个方格里，同时开始向大本营进发。所有参赛队从一个方格移动到另一个无障碍的相邻方格（“相邻”是指两个方格有一条公共边）所花的时间都是 1 个单位时间。但当有多支队伍同时进入大本营时，必将发生火拼，造成参与火拼的所有队伍无法继续比赛。大赛规定：最先到达大本营并能活着夺宝的队伍获得胜利。
假设所有队伍都将以最快速度冲向大本营，请你判断哪个队伍将获得最后的胜利。

##### 输入格式：
输入首先在第一行给出两个正整数 m 和 n（2<m,n≤100），随后 m 行，每行给出 n 个数字，表示地图上对应方格的状态：1 表示方格可通过；0 表示该方格有障碍物，不可通行；2 表示该方格是大本营。题目保证只有 1 个大本营。
接下来是参赛队伍信息。首先在一行中给出正整数 k（0<k<m×n/2），随后 k 行，第 i（1≤i≤k）行给出编号为 i 的参赛队的初始落脚点的坐标，格式为 x y。这里规定地图左上角坐标为 1 1，右下角坐标为 n m，其中 n 为列数，m 为行数。注意参赛队只能在地图范围内移动，不得走出地图。题目保证没有参赛队一开始就落在有障碍的方格里。

##### 输出格式：
在一行中输出获胜的队伍编号和其到达大本营所用的单位时间数量，数字间以 1 个空格分隔，行首尾不得有多余空格。若没有队伍能获胜，则在一行中输出 No winner.

##### 输入样例：
```
5 7
1 1 1 1 1 0 1
1 1 1 1 1 0 0
1 1 0 2 1 1 1
1 1 0 0 1 1 1
1 1 1 1 1 1 1
7
1 5
7 1
1 1
5 5
3 1
3 5
1 4
```
##### 输出样例：
```
7 6
```
##### 样例说明：
七支队伍到达大本营的时间顺次为：7、不可能、5、3、3、5、6，其中队伍 4 和 5 火拼了，队伍 3 和 6 火拼了，队伍 7 比队伍 1 早到，所以获胜。

##### 思路
正面很难做，需要逆着思考，从大本营出发到各个队员出发点，经典的**广度优先搜索**。

##### 个人参考代码
```c++
#include<bits/stdc++.h>
#include<unordered_map>
using namespace std;
#define endl "\n"
void solve() {
	int n, m;
	cin >> n >> m;
	vector<vector<int>> v(n + 5, vector<int>(m + 5)),hax(n + 5, vector<int>(m + 5)),dis(n + 5, vector<int>(m + 5,-1));
	int stax, stay;
	for(int i=1;i<=n;i++)
		for (int j = 1; j <= m; j++) {
			cin >> v[i][j];
			if (v[i][j] == 2) {
				stax = i;
				stay = j;
			}
		}
	int k;
	cin >> k;
	map<int, pair<int,int>> mp;
	for (int i = 1; i <= k; i++) {
		int x, y;
		cin >> y >> x;
		mp[i] = { x,y };
	}
	deque<pair<int,int>>deq,deq2;
	deq.push_back({ stax,stay });
	int disx[4] = {-1,0,1,0};
	int disy[4] = {0,1,0,-1};
	int distt = 0;
	hax[stax][stay] = 1;
	while (!deq.empty()) {
		while (!deq.empty()) {
			int x = deq.front().first, y = deq.front().second;
			dis[x][y] = distt;
			deq.pop_front();
			for (int i = 0; i < 4; i++) {
				if (!hax[x + disx[i]][y + disy[i]] && v[x + disx[i]][y + disy[i]] != 0) {
					deq2.push_back({ x + disx[i],y + disy[i] });
					hax[x + disx[i]][y + disy[i]] = 1;
				}
			}
		}
		deq = deq2;
		deq2.clear();
		distt++;
	}

	map<int, vector<int>>mp2;
	for (int i = 1; i <= k; i++) {
		int x = mp[i].first, y = mp[i].second;
		mp2[dis[x][y]].push_back(i);
	}
	for (auto it : mp2) {
		if (it.second.size() > 1)continue;
		else if (it.first == -1)continue;
		else {
			cout << it.second[0] << " " << it.first;
			return;
		}
	}
	cout << "No winner.";
}
int main() {
	int tt;
	tt = 1;
	while (tt--) {
		solve();
	}
	return 0;
}
```
#### <span style="color:red">3-2~3-3</span>
太难了...