## 1. 问题
给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

示例 1:
```
输入: haystack = "hello", needle = "ll"
输出: 2
```
示例 2:
```
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```
说明:
当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。
## 2. 分析
使用KMP算法，字符串匹配算法，效率高，但是复杂。

## 3. 题解
```C
char *strstr(const char *haystack, const char *needle)
{
    int n;
    if(*needle){
        while(*haystack){
            for(n = 0;*(haystack+n)==*(needle+n);++n){
                if(!*(needle+n+1)){
                    return (char*)haystack;
                }
            }
            haystack++;
        }
        return NULL;
    }
    return (char*)haystack;
}
```
**注：这种写法要超时，性能不佳。建议学习KMP算法**