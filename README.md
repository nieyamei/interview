# interview
收集一些面试题以及自己的答案
> ### 链家
> 1. PHP弱类型的底层实现
> 2. PHP的变量是怎么存储的（这俩问题甩过来，我说不会，源码内核的问题就没再问我了）
> 3. innodb和myisam的特性，区别，用途
> 4. 多列索引的生效规则
> 5. sql语句优化的具体实例
> 6. 二维数组排序
> 7. 字符串内置函数题
> 8. 快速排序，插入排序，二分排序等基础排序算法
```
1. PHP弱类型实现靠底层一个叫zval的一个结构体[ 这个结构体包括 type value is_ref ref_count  其中is_ref 和ref_count 对垃圾回收起重要作用]
2. PHP变量是存储在联合体中 [联合体中的变量类型 有long double str hashtable obj]
> 结构体和联合体的区别
> 结构体(struct)中所有变量是“共存”的——优点是“有容乃大”，全面；缺点是struct内存空间的分配是粗放的，不管用不用，全分配。
> 而联合体(union)中是各变量是“互斥”的——缺点就是不够“包容”；但优点是内存使用更为精细灵活，也节省了内存空间
3. innodb和myisam的特性，区别，用途

typedef struct _zval_struct zval;  
   
struct _zval_struct {  
    /* Variable information */  
    zvalue_value value;     /* value */  
    zend_uint refcount__gc;  
    zend_uchar type;    /* active type */  
    zend_uchar is_ref__gc;  
};  
   
typedef union _zvalue_value {  
    long lval;  /* long value */  
    double dval;    /* double value */  
    struct {  
        char *val;  
        int len;  
    } str;  
    HashTable *ht;  /* hash table value */  
    zend_object_value obj;  
} zvalue_value;

#define IS_NULL     0  
#define IS_LONG     1  
#define IS_DOUBLE   2  
#define IS_BOOL     3  
#define IS_ARRAY    4  
#define IS_OBJECT   5  
#define IS_STRING   6  
#define IS_RESOURCE 7  
#define IS_CONSTANT 8  
#define IS_CONSTANT_ARRAY   9


在PHP中，任何不属于PHP的内建的变量类型的变量，都会被看作资源来进行保存。
比如：数据库句柄、打开的文件句柄、打开的socket句柄。
资源类型，会用lval，此时它是一个整型指示器， 然后PHP会再根据这个指示器在PHP内建的一个资源列表中查询相对应的资源。
```


> 一轮
>  1).mysql  redis mongdb
>  2).php 还会不会其他语言
>  3).消息队列 秒杀场景的应用
>  4).基础算法 数据结构
>  5).然后还有对laravel的了解
> 二轮
>  1).设计模式
>  2).让你把之前项目的架构画出来
>  3).并发 大数据 linux 健康机制
>  4).nginx源码有没有读过 (这里回答没有 面试官直接给了一句 你用nginx源码都没看过 ^这里没有嘲讽的意思 我理解更多的是指出你的不足^)
>  5).swoole会不会？
> 三轮
>   1).你想从事什么相关的工作内容
>   2).喜欢什么样的环境
>   3).这里就是一些你想要什么发展
   
> ### 新浪
> 1.  $a='abcd'; 给出多种方法字符串反转。
> 2. 会不会lua
> 3. 会不会shell
> 4. 遍历文件夹下所有文件
> 5. 查找指定日志文件
> 6. 日志分析

> ### 金融上市公司
> 1. 查找目录下全部文件中是否有test()这个方法。
> 2. 如何在一个数组中找出相同的两个元素
> 3. tp和laravel各方面对比
> 4. laravel各版本之间的不同
> 5. cookie和session

### 总结
> 一线公司bat，还有微博链家这种鸟哥待过的地方，都很注重基础的考核，后面才考的lnmp技术栈。
> 其他公司的面试内容大多在工具，框架使用和web开发常用到的技术上面
