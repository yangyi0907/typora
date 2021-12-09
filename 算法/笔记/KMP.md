```java
public int kmpSearch(String str1, String str2, int[] next) {
    for (int i = 0, j = 0; i < str1.length(); i++) {
        //需要处理 str1.charAt(i) ！= str2.charAt(j), 去调整 j 的大小
        //KMP 算法核心点, 可以验证...
        while (j > 0 && str1.charAt(i) != str2.charAt(j)) {
            j = next[j - 1];
        }
        if (str1.charAt(i) == str2.charAt(j)) {
            j++;
        }
        if (j == str2.length()) {
            return i - j + 1;
        }
    }
    return -1;
}
public int[] kmpNext(String dest) {
    int[] next = new int[dest.length()];
    next[0] = 0;
    for (int i = 1, j = 0; i < dest.length(); i++) {
        //当 dest.charAt(i) != dest.charAt(j) ，我们需要从 next[j-1]获取新的 j
        //直到我们发现 有 dest.charAt(i) == dest.charAt(j)成立才退出
        //核心
        while (j > 0 && dest.charAt(i) != dest.charAt(j)) {
            j = next[j - 1];
        }
        //当 dest.charAt(i) == dest.charAt(j) 满足时，部分匹配值就是+1
        if (dest.charAt(i) == dest.charAt(j)) {
            j++;
        }
        next[i] = j;
    }
    return next;
}
```

[帮你把KMP算法学个通透！B站（理论篇）](https://www.bilibili.com/video/BV1PD4y1o7nd/)

[帮你把KMP算法学个通透！（求next数组代码篇）](https://www.bilibili.com/video/BV1M5411j7Xx)

[KMP算法求next数组](https://www.bilibili.com/video/BV16X4y137qw?from=search&seid=5936320364766248263)