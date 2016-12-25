一、实验内容：

1. 修改example1，使其输出3次方数
2. 修改example2，让3个square模块变成2个

二、实验步骤

1、对example1的修改：

example1需要修改的语句位于square.c文件中：

    if (p->local->index < p->local->len) {
        DOL_read((void*)PORT_IN, &i, sizeof(float), p);
        i = i*i;
        DOL_write((void*)PORT_OUT, &i, sizeof(float), p);
        p->local->index++;
    }
在example1中，计算i的平方的语句是上图中的

	i = i*i;

因此，如果要输出i的3次方数，则只需要将上述语句改为
		
	i = i*i*i;
即可 

**编译并运行修改后的代码**

1. 删除main文件夹下的已存在的example文件，该文件的具体目录为dol/build/bin/main；
2. 在dol目录下使用指令
	ant -f build_zip.xml all
进行编译；
3. 在目录dol/build/bin/main下使用指令为sudo ant -f runexample.xml -Dnumber=1 ### 运行example1

**实验结果**

![](https://raw.githubusercontent.com/zhanggx9/ES2016_14353387/master/lab3/example1_result.png)

如上图所示，已经能够成功输出i的三次方。


2、对example2的修改：

example2需要修改的语句位于example1.xml文件中：
语句

	<variable value="3" name="N"/>

定义了三个square模块，如果只需要两个模块，将value的值改为2即可

**实验结果**

运行修改完的代码后，在目录dol/build/bin/main/example2的文件夹下，找到到example2.dot文件，双击打开，截图如下：

![](https://raw.githubusercontent.com/zhanggx9/ES2016_14353387/master/lab3/example2_dot.png)

由上图可以看出，square模块已经变成了2个。

三、实验感想

这次实验由于TA已经比较详细地讲过了每个example中的源代码，所以我们的工作就减轻了许多，只需要修改对应位置的几行代码即可，不过实验做起来简单，还是要花些时间去认真理解整个代码的。

