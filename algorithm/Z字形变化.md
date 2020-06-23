## 1. 问题
将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。

比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：
```
L   C   I   R
E T O E S I I G
E   D   H   N
```
之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。
请你实现这个将字符串进行指定行数变换的函数：
```
string convert(string s, int numRows);
```

示例 1:
```
输入: s = "LEETCODEISHIRING", numRows = 3
输出: "LCIRETOESIIGEDHN"
```
示例 2:
```
输入: s = "LEETCODEISHIRING", numRows = 4
输出: "LDREOEIIECIHNTSG"
解释:
L     D     R
E   O E   I I
E C   I H   N
T     S     G
```
思路：当前行数是0或者n-1的时候变换上下方向(n为指定行数)

## 2. 分析
从左到右按箭头方向迭代 s ，将每个字符添加到合适的行。之后从上到下遍历行即可。

![t1](file:///E:/github-work/leetcode-training/_image_/d610b140dd0789204efe699672dc72a83e7b826da0165bbf083d24fc97ecdea7-image.png)
## 3. 题解
```C++
class Solution
{
public:
    string convert(string s, int numRows)
    {
        if(numRows == 1)
        {
            return s;
        }
        int sSize = int(s.size());
        int storeSize = min(sSize,numRows);
        string result;
        vector<string> rows(storeSize);
        int curRow = 0;
        //初始有一次更改change值，因此初始值为false
        bool change = false;
        for(char c:s){
            //将第n行的值存在rows[n]中
            rows[curRow] += c;
            if(curRow == 0 || curRow == numRows-1){
                change = !change;
            }
            curRow += change? 1:-1;
        }
        string ret;
        for(string row : rows){
            ret += row;
        }
        return ret;
    }
}
```
知识点：对于string的for循环遍历
```
//处理每个字符串（遍历每个字符串，且对单个字符不做修改，只做判断）基于范围的for语句（C++11新标准）
string str;
for(auto c:str) //c是变量，用于访问str中每一个元素，每次迭代c会初始化为str中的下一个元素；str字符串序列
{ 循环题 }

//处理每个字符串（需要对某些字符做出修改）：如果要改变string对象中字符的值，则必须把循环中的变量定义为引用类型
string str;
for(auto &c:str) //c是变量，用于访问str中每一个元素，每次迭代c会初始化为str中的下一个元素；str字符串序列
{ 循环题 }
```