---
title: 神奇的堆
description: 
published: true
date: 2022-01-26T01:23:20.446Z
tags: 
editor: markdown
dateCreated: 2022-01-26T01:23:17.164Z
---

# 堆——神奇的优先队列
- 堆是一种特殊的完全二叉树，所有父节点都比子节点药效，符合这样的二叉树称之为堆。
- 反之，如果所有父节点都比子节点要大，这样的完全二叉树称为最大堆。

---
# 代码展示
- 此处展示的是向上调整法建立最大堆。
```c
#include<stdio.h>
int a[1000], n;

void siftup(int i)
{
    int flag = 0;//用来标记是否还需要向上调整
    int t;
    if (i == 1)
        return;//如果是堆顶，就不用调整了。
    while (i != 1 && flag == 0)
    {
        //判断是否比父节点大
        if (a[i] > a[i / 2])
        {
            t = a[i];
            a[i] = a[i / 2];
            a[i / 2] = t;
        }
        else
        {
            flag = 1; //表示不需要调整了
        }
        i = i / 2; //这句话很重要，更新编号为i为它父节点的编号，从而便于下一次继续向上调整
    }
}

int main()
{
    int i;
    scanf("%d", &n);

    for (i = 1; i <= n; i++)
    {
        scanf("%d", &a[i]);
        siftup(i);
    }

    for(i=1;i<=n;i++)
    {
        printf("%d ",a[i]);
    }
    return 0;
}

```
运行结果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/bcdb43c39c6545b3a8c38f979e3c532d.png)
- 画出来就是这样，看，是不是变成最大堆了？
- 这里数组里的编号很好理解，遵循从上到下从左到右的原则，依次编号。
- 这样做的好处是，父结点的编号是子节点的1/2（根据向下取整原则，除以二可以正好得到父节点的编号。）
- 这张图我画了好久才画出来~
![在这里插入图片描述](https://img-blog.csdnimg.cn/fbdb953f7d6e4300ab7f2bd6205f448d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ04tRHVzdA==,size_16,color_FFFFFF,t_70,g_se,x_16)

- 如果想要建立最小堆呢？那只需要改一个符号
```c
 if (a[i] < a[i / 2])
```
再运行就是最小堆了~
![在这里插入图片描述](https://img-blog.csdnimg.cn/a97ff94123884cc0b83397802c9727fd.png)


---
# 神奇的堆排序
- 这里用到的是向下调整的方式，和上面不同，但思路类似。
- 堆排序也是一种时间复杂度为`O(nlogn)`的绝佳的排序算法，配合最大堆的使用，原理是每次交换堆顶和队尾的值，每次交换后为了保持最大堆的特性，对堆顶值执行向下调整。
- 这时你可能会问了，那队尾的最大值岂不是会破坏最大堆的特性？
- 所以我们此时把总数`n--`，即：这个队的长度已经-1了，队以外的不是我们堆里的内容。（是已经排好的序列）
- 每次都把最大值往最后丢，然后长度-1。（最大值是哪个？最大值是`a[1]`呀！）
- 直到某一刻`n=1`时，表示这个堆已经被你丢完了，你的排序就完成了。
- 具体代码如下：
```c
#include<stdio.h>
int a[1000], n;


//向下调整函数
void siftdown(int i)
{
    int flag = 0;//用来标记是否还需要调整
    int t;
    //当i结点有儿子
    while (i * 2 <= n && flag == 0)
    {
        //先判断和左儿子的关系
        if (a[i] < a[i * 2])
            t = i * 2;
        else
            t = i;
        //有右儿子吗
        if (i * 2 + 1 <= n)
        {
            //有右儿子，而且发现右儿子是父子中最大的
            if (a[t] < a[i * 2 + 1])
                t = i * 2 + 1;
        }
        //以上过程就是找父子一家人里最大的那个
        //如果发现最大结点编号不是自己的，说明子节点中有比父节点更大的，交换它们！
        int temp;
        if (t != i)
        {
            temp = a[t];
            a[t] = a[i];
            a[i] = temp;
            i = t; //更新i为最大结点编号，便于接下来继续向下调整
        }
        else
            flag = 1;//表示不需要调整了
    }
}

void heapsort()
{
    int temp;
    while (n > 1)
    {
        temp = a[1];
        a[1] = a[n];
        a[n] = temp;
        n--;
        siftdown(1);
    }
}

void creat()
{
    int i;
    //从最后一个非叶子结点开始向上调整
    for (i = n / 2; i >= 1; i--)
    {
        siftdown(i);
    }
}

int main()
{
    int i, num;
    scanf("%d", &n);
    num = n;
    for (i = 1; i <= n; i++)
        scanf("%d", &a[i]);

    creat();

    //堆排序
    heapsort();

    for (i = 1; i <= num; i++)
    {
        printf("%d ", a[i]);
    }
    return 0;
}

```

运行结果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/c843240736524e1ea9d5e621cf7530f9.png)
- 神奇！你的排序到此就完成了！
- 所以你更喜欢快排还是堆排序呢？（反正我是堆排序）
> 在此，《啊哈！算法》的前7章内容已经结束了，非常感谢纪磊老师，让我这么多年以来一直热爱着研究算法。
