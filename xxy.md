# <font face="华文彩云" size=150%>单链表</font>







[toc]

 



## 一、链表是什么？

> ​    链表是一种物理存储单元上非连续、非顺序的存储结构，数据元素的逻辑顺序是通过链表中的指针链接次序实现的。链表由一系列结点（链表中每一个元素称为结点）组成，结点可以在运行时动态生成。每个结点包括两个部分：一个是存储数据元素的数据域，另一个是存储下一个结点地址的指针域。 

## 二、为什么要使用链表

在未学习链表之前，我们常用的数据储存方式为数组。而数组的好处与弊端也非常明显：

>**顺序存储（数组）：**
>		**优点：**
>
>+ 用数组存储数据元素，操作方法简单，容易实现。
>+ 无需为表示结点间的逻辑关系而增加额外的存储开销。数组可按元素位序随机存储结点。
>  **缺点：**
>
>	+ 做插入删除时需要大量的移动数据元素，效率较低。
>	+ 要占用连续的存储空间，内存分配只能预先进行。如果估计过大，造成内存浪费，估计过小，数据存不下。

链表的优缺点：

> **链式存储（链表）：**
>   	 **优点：**
>
>  + 不用事先估计存储规模，随用随开辟。
>
>  + 做插入、删除时不需要大量的移动数据元素，效率较高。
>
>    **缺点：**
>
>  + 查询只能遍历查找，效率较低。
>
>  + 需要为表示结点间的逻辑关系而增加额外的存储开销。
>
>  + 不能随机访问，只能顺序访问。

## 三、创建链表前的准备

**首节点**：存放第一个有效数据的结点

**头节点**：在单链表的第一个结点之前附设一个结点，它的数据域不存储任何信息，指针域指向第一个结点的地址。

**头指针**：指向头结点的指针

**尾结点**：存放最后一个有效数据的结点

**尾指针**：指向尾结点的指针

## 四、单链表的创建

### 1）准备每一个结点的数据 <font color='red'>(使用结构体)</font>

如：

```
typedef struct node{
      char name[20];
      int number;
      struct node *next;  
}Node,*LinkList;
```

<font color=#FF0000> 必须以分号结尾 </font>   

### 2）单链表初始化 <font color='red'>（创建头结点）</font>

```
LinkList InitList(){
	  LinkList head;
	  head=(Node*)malloc(sizeof(Node));
	  head->next=NULL;
	  return head;
}
```

### 3）单链表的建立<font color='red'>（尾插法）</font>

```
void CreatByRear(LinkList head){
	 Node *r,*s;
	 char name[20];
	 int number;
	 r=head;
	 printf("请输入学生的姓名和学号：\n")；
	 while(1)
	 {
	 scanf("%s",name);
	 scanf("%d",&number);
	 if(number==0)
	 	break;
	 s=(Node*)malloc(sizeof(Node));
	 strcpy(s->name,name);
	 s->number=number;
	 r->next=s;					/*原来的结点指向新结点*/
	 r=s;						/*r指向新结点*/
	 }
	 r->next=NULL;				/*链表的尾指针为空*/
}
```

### 4）单链表的遍历

```
void OutPut(LinkList head){
	 Node *p;					/*循环用的临时指针*/
	 p=head->next;				/*p指向链表的首元结点*/
	 while(p)
	 {
	 	printf("姓名：%s\n",p->name);
	 	printf("学号：%d\n",p->number);
	 	p=p->next;
	 }
}
```

### 5）单链表的插入

```
void Insert (LinkList head,int i)
{
	 Node *p=head,*s;
	 int j=0;
	 while(j<i-1&&p)
	 {
	 	p=p->next;
	 	j++;
	 }
	 if(p)
	 {
	 s=(Node*)malloc(sizeof(Node));
	 scanf("%s",s->next);
	 scanf("%d",&s->number);
	 s->next=p->next;
	 p->next=s;
	 }
}
```

### 6）单链表的删除

```
void Delete(LinkList head,int pos)
{
	 Node *p=head,*q;
	 int j=0;
	 while(j<pos-1&&p)    /*通过循环，找到第pos-1个结点的地址p*/
	 {
	 	p=p->next;
	 	j++;
	 }
	 if(p==NULL||p->next==NULL)/*第pos个结点不存在*/
	 {
	 	printf("the pos is error");
	 }
	 else
	 {
	 	q=p->next;        /*q指向第pos个结点*/
	 	p->next=q->next;  /*连接删除结点两边的结点*/
	 	free(q);          /*释放要删除结点的内存空间*/
	 }
}
```

### 7）单链表的查询

```
Node* Search(LinkList head,char name[])
{
	 Node *p=head->next;
	 while(p)
	 {
	 	if(strcmp(p->name,name)!=0)
	 		p=p->next;
	 		else
	 		break;
	 }
	 if(p==NULL)
	 {
	 	printf("没有找到结点")；
	 }
	 return p;
}
```

###  8）单链表的长度

```
int ListLength(LinkList head)
{
	 int count=0;
	 Node *p;
	 p=head->next;
	 while(p)
	 {
	 	count++;
	 	p=p->next;
	 }
	 return count;
}
```

:sweat_smile:~~**该摆还得摆**~~



### 	







