# 本页面含有高精加，乘法
## 高精加

```
#include <bits/stdc++.h>
using namespace std;
string a,b,c;
int main(){
    ios::sync_with_stdio(0);
    cin.tie();
    cout.tie();
    cin>>a>>b;
    while(a.length()<b.length()) a='0'+a;
    while(b.length()<a.length()) b='0'+b;
    int len=a.length();
    int jw=0;
    for(int i=len-1;i>=0;i--){
        int t1,t2,t;
        t1=a[i]-48;t2=b[i]-48;
        t=t1+t2+jw;
        jw=t/10;
        t%=10;
        c=char(t+48)+c;
    }
    if(jw)
        c='1'+c;
    cout<<c;
    return 0;
}
```

### 本质原理就是字符串竖式加法
怎么个说法呢？
 ```
while(a.length()<b.length()) a='0'+a;
 while(b.length()<a.length()) b='0'+b;
```
这段是在两个数字中较短的那个前补足0
如
 `12345 1234 -> 12345 01234`
`int jw=0;`
"jw" 进位，顾名思义，判断数组的下一位是否需要进位
 ```
int t1,t2,t;
 t1=a[i]-48;t2=b[i]-48;
 t=t1+t2+jw;
 jw=t/10;
 t%=10;
 c=char(t+48)+c;
```
### 一行一行来
t1 数字a某一位的“数字”形式
t2 数字b某一位的“数字”形式
t t1+t2+jw 顾名思义，不做赘述
然后jw赋值成下一位的进位，t只取余数，填入结果数组c中

## 好了，更复杂的高精乘来了

```
#include <bits/stdc++.h>
using namespace std;
string a1,b1;
int a[2005],b[2005],len,c[10005];
int main(){
    cin>>a1>>b1;
    int lena=a1.length();
    int lenb=b1.length();
    for(int i=1;i<=lena;i++) a[i]=a1[lena-i]-'0';
    for(int i=1;i<=lenb;i++) b[i]=b1[lenb-i]-'0';
    for(int i=1;i<=lena;i++)
        for(int j=1;j<=lenb;j++)
            c[i+j-1]+=a[i]*b[j];
    for(int i=1;i<=lena+lenb;i++)
        if(c[i]>=10){
            c[i+1]+=c[i]/10;
            c[i]%=10;
        }
    len=lena+lenb;
    while((c[len]==0)&&len>1) len--;
    for(int i=len;i>=1;i--) cout<<c[i];
    return 0;
}
```
### 按位乘法+高精加
### 啥，你问我具体原理？
### 我  不  想  写


# 更详细的原理可以来看这个 来自OIwiki 更完美，更详细，更易懂，还带图
# <https://oi-wiki.org/math/bignum/#%E9%AB%98%E7%B2%BE%E5%BA%A6%E9%AB%98%E7%B2%BE%E5%BA%A6>