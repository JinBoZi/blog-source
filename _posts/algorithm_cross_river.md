title: 逻辑推理中的过河问题-C++代码解决方法
tags:
- 递归算法
- 逻辑题
categories:
- code
- C++
comments: true
description: 师兄前天做了一道面试题，“一个警察,一个犯人,爸爸,两个小男孩,妈妈,两个小女孩,要过河.妈妈爸爸警察会划船.爸爸不在,妈妈会伤害男孩.妈妈不在,爸爸会伤害女孩.警察不在,犯人会伤害家人.船上最多能坐两个人.问怎样过河”，由于没有在规定时间内得出逻辑推理的解答，面试官让师兄写代码实现，我一时兴起，便有了这篇博客。
---

## **问题描述：** ##

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;话说有一家六口人，包括爸爸、妈妈、两个女儿及两个儿子在旅行途中迷了路，还不幸遇上了一个逃狱的犯人，幸好犯人让一个也在旅行的警察逮捕，一家六口才得以保住性命。他们只有通过一条河流方能回家，能帮帮他们么？

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;玩家的任务是，帮助这些人渡过河，交通工具只有一艘小船。只有爸爸、妈妈以及警察能控制小船，此外，不论成人或是小孩，小船每次最多只能搭乘二人。在渡河期间，玩家还要防止以下三种情况发生：

1、当警察与犯人分开时，犯人会伤害一家六口。
2、当爸爸看见妈妈离开女儿时，爸爸便会教训女儿。
3、当妈妈看见爸爸离开儿子时，妈妈便会教训儿子。


## **正确答案：** ##

1)警察带小偷先过河的对面，然后警察把小偷放下自己回来； 
2)警察再带儿子A过河，将儿子A放下，把小偷带回来； 
3)爸爸带儿子B过河，将儿子B放下，自己回来； 
4)爸爸带妈妈过河，上岸后，妈妈自己回来； 
5)警察再带小偷过河，警察和小偷都上岸，爸爸回来； 
6)爸爸和妈妈再过河，妈妈自己回来； 
7)妈妈带女儿A过河，妈妈和女儿A都上岸，警察带小偷回来； 
8)警察带女儿B过河，女儿B上岸后，警察自己回来； 
9)警察再带小偷过河就可以了。


## **主要思路：** ##

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;递归实现，在每一次递归中，若判断出所有人都已过岸，则层层返回并在返回过程中打印结果；若还未成功过岸，遍历所有可能的过河方案，进入下一层递归；若过岸成功，打印结果，若过岸失败，则还原状态，继续循环检查下一状态。
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;检查函数中主要判断是否存在几个伤害情况。过河前，警察要上船，犯人还留在岸上，且有其他家人在岸上；爸爸要上船，妈妈还留在岸上，且有儿子还在岸上；妈妈要上船，爸爸还留在岸上，且有女儿还在岸上。过河后，下船后，若警察不在本岸，犯人却在本岸，且有其他人在本岸；若爸爸不在本岸，妈妈却在本岸，且有儿子在本岸；若妈妈不在本岸，爸爸却在本岸，且有女儿在本岸。这些情况都会导致过河失败，应还原状态。


## **代码实现：** ##

```C++
#include<cstdio>

using namespace std;

int passager_one[15] = {0 ,0,0,0,0,0,0,0,1 ,1,1,1,2 ,2,2};
int passager_two[15] = {-1,1,2,3,4,5,6,7,-1,2,4,5,-1,6,7};

int bank[16] = {1,1,1,1,1,1,1,1,0,0,0,0,0,0,0,0};

int which_bank = 0;

int check(int one,int two)
{
	if(bank[which_bank+one]==0 || (two!=-1 && bank[which_bank+two]==0))return 0;
	//printf("%d %d\n",one,two);
	bank[which_bank+one]=0;
	if(two!=-1)bank[which_bank+two]=0;
	if(one==0 && bank[which_bank+3]==1 && (bank[which_bank+1]||bank[which_bank+2]||bank[which_bank+4]||bank[which_bank+5]||bank[which_bank+6]||bank[which_bank+7])){
		bank[which_bank+one]=1;
		if(two!=-1)bank[which_bank+two]=1;
		return 0;
	}
	if((one==1||two==1) && bank[which_bank+2]==1 && (bank[which_bank+4]||bank[which_bank+5])){
		bank[which_bank+one]=1;
		if(two!=-1)bank[which_bank+two]=1;
		return 0;
	}
	if((one==2||two==2) && bank[which_bank+1]==1 && (bank[which_bank+6]||bank[which_bank+7])){
		bank[which_bank+one]=1;
		if(two!=-1)bank[which_bank+two]=1;
		return 0;
	}
	which_bank = (which_bank+8)%16;
	bank[which_bank+one]=1;
	if(two!=-1)bank[which_bank+two]=1;

	if(bank[which_bank]==0 && bank[which_bank+3]==1 && (bank[which_bank+1]||bank[which_bank+2]||bank[which_bank+4]||bank[which_bank+5]||bank[which_bank+6]||bank[which_bank+7])){
		bank[which_bank+one]=0;
		if(two!=-1)bank[which_bank+two]=0;
		which_bank = (which_bank+8)%16;
		bank[which_bank+one]=1;
		if(two!=-1)bank[which_bank+two]=1;
		return 0;
	}
	if(bank[which_bank+1]==0 && bank[which_bank+2]==1 && (bank[which_bank+4]||bank[which_bank+5])){
		bank[which_bank+one]=0;
		if(two!=-1)bank[which_bank+two]=0;
		which_bank = (which_bank+8)%16;
		bank[which_bank+one]=1;
		if(two!=-1)bank[which_bank+two]=1;
		return 0;
	}
	if(bank[which_bank+2]==0 && bank[which_bank+1]==1 && (bank[which_bank+6]||bank[which_bank+7])){
		bank[which_bank+one]=0;
		if(two!=-1)bank[which_bank+two]=0;
		which_bank = (which_bank+8)%16;
		bank[which_bank+one]=1;
		if(two!=-1)bank[which_bank+two]=1;
		return 0;
	}

	return 1;
}

int cross_river(int last_passagers)
{
	//printf("bank:%d",which_bank);
	//getchar();
	if(which_bank == 8){
		int temp_sum=0;
		for(int index=8;index<16;index++)temp_sum+=bank[index];
		if(temp_sum == 8)return 1;
	}
	for(int index=0;index<15;index++){
		if(index!=last_passagers && check(passager_one[index],passager_two[index])){
				//printf("%d %d %d\n",passager_one[index],passager_two[index],which_bank);
		//getchar();
			if(cross_river(index)){
				printf("%d %d %d\n",passager_one[index],passager_two[index]);
				return 1;
			}
			else{
				bank[which_bank+passager_one[index]]=0;
				if(passager_two[index]!=-1)bank[which_bank+passager_two[index]]=0;
				which_bank = (which_bank+8)%16;
				bank[which_bank+passager_one[index]]=1;
				if(passager_two[index]!=-1)bank[which_bank+passager_two[index]]=1;
			}
		}
	}
	return 0;
}

int main()
{
	cross_river(-1);
}
```

