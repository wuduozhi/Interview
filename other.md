# 字符编码

* [字符编码笔记：ASCII，Unicode 和 UTF-8](http://www.ruanyifeng.com/blog/2007/10/ascii_unicode_and_utf-8.html)

# 缓存 cache

* [漫画：要跳槽？这道缓存设计题你有必要看看!](https://mp.weixin.qq.com/s/hmBxNoQSHiWIWNa3WLzrfw)
* [https://coolshell.cn/articles/17416.html](https://coolshell.cn/articles/17416.html)

## 缓存更新


* 先删除缓存，再更新数据库

对于一个更新操作简单来说，就是先去各级缓存进行删除，然后更新数据库。这个操作有一个比较大的问题，在对缓存删除完之后，有一个读请求，这个时候由于缓存被删除所以直接会读库，读操作的数据是老的并且会被加载进入缓存当中，后续读请求全部访问的老数据。

![image](https://user-gold-cdn.xitu.io/2018/8/22/165600e478a0aea7?imageView2/0/w/1280/h/960/ignore-error/1)

* 先更新数据库，再删除缓存(推荐)

