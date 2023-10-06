---
title: "ACM-ICPC Asia Qingdao Regional Contest, Online"
author: xy
date: 2018-09-17 22:00:00 +0800
categories: [Archive]
tags: [Codes]
img_path: /images/Archive
---

![ICPCQingdaoOnline](/ICPCQingdaoOnline.png)

---

前言：

昨天参加了一波青岛赛区的ACM网络赛，很快乐的水了一下午，感觉自己一直不在状态。

只做出来五道题，C题思路有问题，WA了几次，超时了几次，罚时罚到爆炸。

简单记录一下五道题的思路和代码。


Problem A. Live Love：

非常水的一道题，本质就是一个数列问题，求数列中特殊值的连续个数最大值和最小值，纯模拟。

代码如下：

```
using namespace std;
int main() {
int T, n, m, mx, mn, a[105], w;
cin >> T;
while (T–) {
int sum = 0, k = 0;
for (int i = 0; i < 105; i++) a[i] = 0; scanf("%d%d", &n, &m); if (n == m) { mx = m; mn = m; } else if (m == 0) { mx = 0; mn = 0; } else { k = n - m; mx = m; w = n / (k + 1); mn = w; } cout << mx << " " << mn << endl; } }
```
 Problem C. Halting Problem 这道题看起来是个普通的模拟，但实际编写的时候一定要注意输入和输出还有循环跳出的复杂度。因为奇葩的数据，我前13次提交都没通过。
```
#include
#include
#include
using namespace std;
string s[7];
string cz[11000];
int y[11000][2];
int c[11000][300];

int main()
{
int i, j, T, n, cnt, x, k, p;
bool b;
string ss;
scanf(“%d”, &T);
s[1] = “add”;
s[2] = “beq”;
s[3] = “bne”;
s[4] = “blt”;
s[5] = “bgt”;
while (T–)
{
b = 0;
cnt = 0;
scanf(“%d”, &n);
for (i = 1; i <= n; ++i) for (j = 0; j < 256; ++j) c[i][j] = 0; for (i = 1; i <= n; ++i) { cin>>cz[i];
if (cz[i] != s[1]) scanf(“%d%d”, &y[i][0], &y[i][1]);
else scanf(“%d”, &y[i][0]);
}
p = 1;
while (p <= n) { if (c[p][cnt]) { b = 1; break; } c[p][cnt] = 1; if (cz[p] == s[1]) { cnt = (cnt + y[p][0]) % 256; ++p; } else if (cz[p] == s[2]) { if (cnt == y[p][0]) p = y[p][1]; else ++p; } else if (cz[p] == s[3]) { if (cnt != y[p][0]) p = y[p][1]; else ++p; } else if (cz[p] == s[4]) { if (cnt < y[p][0]) p = y[p][1]; else ++p; } else { if (cnt > y[p][0]) p = y[p][1];
else ++p;
}
}
if (b) printf(“No\n”);
else printf(“Yes\n”);
}
return 0;
}
```

Problem J. Press the Button

应该是由经典问题“开关灯”演变而来，是一个逻辑和数学的模拟。

```
using namespace std;

long long gcd(long long x, long long y)
{
if (y == 0) return x;
return gcd(y, x % y);
}

void swap(long long &x, long long &y)
{
long long t = x;
x = y;
y = t;
}

int main()
{

int T;
long long v, t, cir, a, c, ans, i, j, b, d;
bool bb;
scanf(“%d”, &T);
while (T–)
{
ans = 0;
bb = 0;
scanf(“%lld%lld%lld%lld%lld%lld”, &a, &b, &c, &d, &v, &t);
cir = a * c / gcd(a, c);
if (a > c)
{
swap(a, c);
swap(b, d);
}
i = 0, j = 0;
ans += b + d – 1;
while ((i + a < cir && i + a <= t) || (j + c < cir && j + c <= t)) { if (i == j) { i += a; if (i - j <= v) ans += b; else ans += b - 1; } else if (i + a <= j + c) { i += a; if (i >= j)
{
if (i – j <= v || a <= v) ans += b; else ans += b - 1; } else { if (a <= v) ans += b; else ans += b - 1; } } else { j += c; if (j - i <= v) ans += d; else ans += d - 1; } } // i -= a; // j -= c; if (cir - i <= v || cir - j <= v) bb = 1; if (cir > t)
{
printf(“%lld\n”, ans);
continue;
}

if (bb) ans = (t / cir) + t / cir * ans;
else ans = t / cir * ans;
t = t % cir;
ans += b + d – 1;
i = 0, j = 0;
while (i + a <= t || j + c <= t) { if (i == j) { i += a; if (i - j <= v) ans += b; else ans += b - 1; } else if (i + a <= j + c) { i += a; if (i >= j)
{
if (i – j <= v || a <= v) ans += b; else ans += b - 1; } else { if (a <= v) ans += b; else ans += b - 1; } } else { j += c; if (j - i <= v) ans += d; else ans += d - 1; } } printf("%lld\n", ans); } return 0; }
```
 Problem H. Traveling on the Axis 同样是一个数学问题，注意单个数据大小和数据总量控制即可。 
```
#include
#include
using namespace std;

long long a[1100000];
char s[1100000];

int main()
{
int T, n, i, len;
long long ans;
scanf(“%d”, &T);
while (T–)
{
ans = 0;
scanf(“%s”, s);
len = strlen(s);
if (s[0] == ‘0’) a[0] = 2, ans = 2;
else a[0] = 1, ans = 1;
for (i = 1; i < len; ++i) if (s[i] == '0') { if (s[i] != s[i - 1]) a[i] = a[i - 1] + i + 2; else a[i] = a[i - 1] + i * 2 + 2; ans += a[i]; } else { if (s[i] != s[i - 1]) a[i] = a[i - 1] + i + 1; else a[i] = a[i - 1] + i * 2 + 1; ans += a[i]; } printf("%lld\n", ans); } return 0; }
```
 Problem K. XOR Clique 水题，纯模拟，得分看手速。 
```
#include
#include
using namespace std;

long long a[1100000];
char s[1100000];

int main()
{
int T, n, i, len;
long long ans;
scanf(“%d”, &T);
while (T–)
{
ans = 0;
scanf(“%s”, s);
len = strlen(s);
if (s[0] == ‘0’) a[0] = 2, ans = 2;
else a[0] = 1, ans = 1;
for (i = 1; i < len; ++i) if (s[i] == '0') { if (s[i] != s[i - 1]) a[i] = a[i - 1] + i + 2; else a[i] = a[i - 1] + i * 2 + 2; ans += a[i]; } else { if (s[i] != s[i - 1]) a[i] = a[i - 1] + i + 1; else a[i] = a[i - 1] + i * 2 + 1; ans += a[i]; } printf("%lld\n", ans); } return 0; }
```
 以上。