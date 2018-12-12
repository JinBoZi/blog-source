title: Python脚本实现文件夹材料重排版
tags:
- 数据处理
categories:
- code
- Python
comments: true
mathjax: true
description: 本学期是数据库助教，在最后整理材料提交给老师的时候，老师说格式不对，文件夹层级结构不对。既然是Ctrl+C,Ctrl+V的重复工作，如果人工操作，容易出错也很繁琐，所以就想用bat编程实现，后来发现bat编程各种处理不太友好（应该是自身实力所限），最后想起还有Python这个好东西，所以就有了以下代码。
---

## **预期目标：** ##

原文件夹层级结构：
根目录
&nbsp;&nbsp;代码
&nbsp;&nbsp;&nbsp;&nbsp;学生代码文件夹
&nbsp;&nbsp;实验报告
&nbsp;&nbsp;&nbsp;&nbsp;助教文件夹
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;学生实验报告文件夹
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;学生八次实验报告

目标文件夹层级结构：
根目录
&nbsp;&nbsp;助教文件夹
&nbsp;&nbsp;&nbsp;&nbsp;学生文件夹
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;学生代码文件夹
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;学生八次实验报告


## **主要思想：** ##

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;因为只有“助教文件夹”才能准确分开各个“学生文件夹”，所以先遍历“助教文件夹”下的所有目录名，以此匹配“代码”下的“学生代码文件夹”，再将每个学生两个文件夹下的材料都拷贝至新的文件夹结构内，最终完成了文件层级结构的转变。


## **代码实现：** ##

```Python
import os
import os.path
import shutil

old_path = "I:\\U10P31010.02"#整理前的文件材料根路径
new_path = "I:\\U10P31010.02(309-3)"#整理后文件材料保存的根路径

'''
作用：判断两文件名是否匹配(由于只需判断10位的学号，所以并没写兼容性很好的函数)
val1：第一个文件名
val2：第二个文件名
返回值：1表示匹配，0表示不匹配
'''
def myEquel(val1,val2):
    for i in range(0,10):
        if(val1[i] != val2[i+3]):
            return 0
    return 1

'''
变量含义
   assistent：助教文件夹的名字
   student_report：报告文件夹名字
   student_code：代码文件夹名字
'''
#第一层循环 找到助教文件夹的名字，按助教分类
for assistent in os.listdir(old_path+"\\实验报告"):
    #开始在新目录下整理，创建相应的助教文件夹
    if not os.path.exists(new_path+"\\"+assistent):
        os.makedirs(new_path+"\\"+assistent)
    #第二层循环 查找每个助教文件夹下所有学生的文件夹名
    for student_report in os.listdir(old_path + "\\实验报告\\" + assistent):
        #第三层循环 匹配每个学生的实验报告文件夹与代码文件夹
        for student_code in os.listdir(old_path + "\\代码"):
            if(myEquel(student_report,student_code) == 1):
                #如果匹配，将材料转移到新目录
                if not os.path.exists(new_path + "\\" + assistent + "\\" + student_code + "\\代码"):
                    os.makedirs(new_path + "\\" + assistent + "\\" + student_code + "\\代码")
                #使用了系统的复制命令xcopy，感觉会快一点/e表示复制文件夹下所有内容 /y表示若重复可覆盖 “> G:\\log.txt 2>&1”是为了屏蔽系统命令的提示信息
                os.system("xcopy " + old_path + "\\代码\\" + student_code + " " + new_path + "\\" + assistent + "\\" + student_code + "\\代码 /e /y > G:\\log.txt 2>&1")
                os.system("xcopy " + old_path + "\\实验报告\\" + assistent +"\\" + student_report + " " + new_path + "\\" + assistent + "\\" + student_code + " /e /y > G:\\log.txt 2>&1")
                #打印提示信息
                print(student_code+" is OK!\n")
                break

```

## **总结：** ##

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;代码还有许多不完善的地方，比如说函数写的太仓促，没有兼容性，代码也不太适合复用于其他场景。但感觉既然写了，就应该好好记录一下，权当积累一些经验吧~



1、[python 获取当前文件夹下所有文件名](https://www.cnblogs.com/strongYaYa/p/7200357.html)
2、[Python创建目录文件夹](https://www.cnblogs.com/monsteryang/p/6574550.html)
3、[Python中执行系统命令常见的几种方法](https://www.cnblogs.com/zflibra/p/4180796.html)
4、[CMD命令——拷贝文件夹](https://blog.csdn.net/victoriaw/article/details/65446791)