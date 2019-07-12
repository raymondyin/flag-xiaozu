## Leetcode Algorithm Problem Detailed Analysis

### Ground Rules
* Would be great if follow Description -> Analysis -> Solution Sample


### 443. String Compression
#### Description
* Input: str = "aabcccccaaa", Output: "a2b1c5a3"
* input: "aabbcc", output: "aabbcc"
#### Analysis

* 如果压缩过的字符串不比原来小, 返回原来的
* 若下一个不等于当前i，那么 chars[i]就是同组别最后一个
  * 所以需要用双指针，一个 runner 跑遍 array，一个用来标记最后一个
  * 边跑还要边记录有几个重复,比如aaa要记录 count = 3
    * 大while里套的小 while 是用来数 count 的
    * 是 two sum 去重的 while 套路
    * 这里不需要chars[runner] == chars[runner+1] 因为runner在最后必然被++，刚刚从 while 进去时，runner 是刚刚被+过的
* 若要求inplace，最后还需要第三write指针，用来加入东西，比如a11
  * write指针套路: 写进去一个,write++

```java
public int compress(char[] chars) {
    int indexAns = 0;
    int runner = 0;
    while (runner < chars.length) {
        char currentChar = chars[runner];
        int count = 0;
        while (runner < chars.length && chars[runner] == currentChar) { //中心句
            runner++;
            count++;
        }
        
        // 起头
        chars[indexAns] = currentChar;
        indexAns++；

        // 头后面加count, e.g. a2
        if(count != 1) {
            for(char c : Integer.toString(count).toCharArray()) {
                chars[indexAns] = c;
                indexAns++;
            }   
        }
    }
    return indexAns;
}
```