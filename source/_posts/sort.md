---
title: 排序算法的比较
date: 2017-09-14 23:11:45
tags: [cpp,算法]
---
排序算法众多，好的算法能大大提高计算效率，提升计算机的运行时间，这里我列出几种简单的排序算法并进行简单的比较。
  
  ---
#### 选择排序
> 在选择排序里，第一次排序将第一个数字和剩下最小的数字进行位置交换，第二次排序将第二个数字和剩下最小的数字交换位置，依此类推直到排序完成。
> 在排序过程中共进行了n(n-1)/2次比较，互相交换了n-1次。选择排序简单易实现，适用于数量较小的排序。
<!--more-->
```
#include<iostream>
using namespace std;
void swap(int &a,int &b)
{
    int temp=a;
    a=b;
    b=temp;
}
int main()
{
    int i,j;
    int a[10];
    int iTemp;
    int iPos;
    cout<<"为数组元素赋值:"<<endl;
    for(i=0;i<10;i++)
        cin>>a[i];

    for(i=0;i<9;i++){
        iTemp=a[i];
        iPos=i;
        for(j=i+1;j<10;j++){    //i=0时将第一个数与后面所以数做对比若找到比a[i]小的数则交换位置
            if(a[j]<iTemp)
            {                   //记录后面作对比的最小的数
                iTemp=a[j];
                iPos=j;
            }
        }
        swap(a[i],a[iPos]);
    }

    for(i=0;i<10;i++){
        if(i==0)
            cout<<"排序后结果"<<endl;
        else   
            cout<<" ";
        cout<<a[i];
        if(i==9)    
            cout<<endl;
        
    }
    return 0;
}

```
#### 冒泡排序
> 在冒泡排序里，第一次排序将最小的数字移动到第一的位置并将其他数字后移，第二次排序将剩下最小的数字移动到第二位并将其他数字后移。
> 冒泡排序最好的情况是正序，因此只要一次比较即可，最坏的情况是逆序，需要比较n^2次。冒泡排序是稳定的排序方法，当待排序列有序时，效果比较好。
```
#include<iostream>
using namespace std;
void swap(int &a,int &b)
{
    int temp = a;
    a = b;
    b = temp;
}
int main()
{
    int i,j;
    int a[10];
    cout<<"为数组元素赋值:"<<endl;
    for(i=0;i<10;i++)
        cin>>a[i];

    for(i=0;i<10;i++){          //将每轮交换后的结果依次放入a[i]中
        for(j=9;j>=i;j--){     
            if(a[j]<a[j-1]){    //从最后一个数开始如果后一个数比前一个数搭则交换
                swap(a[j],a[j-1]);
            }
        }
    }
    for(i=0;i<10;i++){
        if(i==0)
            cout<<"排序后结果"<<endl;
        else   
            cout<<" ";
        cout<<a[i];
        if(i==9)    
            cout<<endl;
        
    }
    return 0;
}
```
*冒泡排序动图*
![](http://louiszhai.github.io/docImages/sort05.gif)
#### 交换排序
> 在排序中将第一个数字与依次后边的数字依次进行比较大于则交换小于则保持原位不变，依此类推第二个数字第三个数字直到排序完成。
> 交换排序与冒泡排序类似，正序是最快，逆序时最慢，有序是效果最好。
```
#include<iostream>
using namespace std;
void swap(int &a,int &b)
{
    int temp = a;
    a = b;
    b = temp;
}
int main()
{
    int i,j;
    int a[10];
    cout<<"为数组元素赋值:"<<endl;
    for(i=0;i<10;i++)
        cin>>a[i];

    for(i=0;i<9;i++){          
        for(j=i+1;j<10;j++){     
            if(a[j]<a[i]){    //a[i]与其后所有值比，后面的数如果比a[i]小的则交换
                swap(a[j],a[i]);
            }
        }
    }
    for(i=0;i<10;i++){
        if(i==0)
            cout<<"排序后结果"<<endl;
        else   
            cout<<" ";
        cout<<a[i];
        if(i==9)    
            cout<<endl;
        
    }
    return 0;
}
```
#### 插入排序
> 将第一个取出然后插入，接着将第二个数取出若小于前一个数则在其前面插入，若大于前一个数则在其后插入，继续取出第三个数，然后与前一个数作比较若大于前一个数则在其后插入，若小于前一个数则继续与前面的数进行比较直到大于前一个数或则到达第一个位置才插入。
> 此算法需要经过n-1次插入过程，如果原始数据基本有序则具有较快的运算速度。
```
#include<iostream>
using namespace std;
int main()
{
    int i,j;
    int a[10];
    int iTemp;
    int iPos;

    cout<<"为数组元素赋值:"<<endl;
    for(i=0;i<10;i++)
        cin>>a[i];

    for(i=1;i<10;i++){
        iTemp=a[i];
        iPos=i-1;
        while(iPos>=0 && iTemp<a[iPos]){
            a[iPos+1] = a[iPos];        //把前一个的值赋给后一个
            iPos--;                     //然后接着与前面的数对比
        }
        a[iPos+1] = iTemp;
    }

    for(i=0;i<10;i++){
        if(i==0)
            cout<<"排序后结果"<<endl;
        else   
            cout<<" ";
        cout<<a[i];
        if(i==9)    
            cout<<endl;
        
    }
    return 0;
}
```
#### 折半排序
> 首先取出左右两边数与中间值进行对比，如果左侧取出的值比中间值小则取下一个元素与中间值比较，右侧同理相反，直到左侧的大于中间值右侧的小于中间值后交换该左右值。直至左边的数均比中间值小右侧均比中间值到。按这方法依次递归左右两边的数。
> 折半排序对于n较大是，具有最快的排序速度。但当n很小时此方法则往往比其他排序算法要慢，不够稳定
```
#include<iostream>
using namespace std;
void swap(int &a,int &b);
void CelerityRun(int left,int right,int array[]);
int main()
{
    int i;
    int a[10];
    cout<<"为数组元素赋值:"<<endl;
    for(i=0;i<10;i++)
        cin>>a[i];

    CelerityRun(0,9,a);

    for(i=0;i<10;i++){
        if(i==0)
            cout<<"排序后结果"<<endl;
        else   
            cout<<" ";
        cout<<a[i];
        if(i==9)    
            cout<<endl;
        
    }
    return 0;
}

void CelerityRun(int left,int right,int array[])
{
    int i,j;
    int middle;
    i = left;
    j = right;
    middle = array[(left+right)/2];
    do{ //第一次折半排序后大于middle的在右边小于middle的在左边
        while((array[i]<middle) && i<right)
            i++;    //比middle小则i++,比middle大则等待与右边比middle小的数交换
        while((array[j]>middle) && j>left)
            j--;
        if(i<=j)
        {
            swap(array[i],array[j]);
            i++;
            j--;
        }
    }while(i<=j);

    if(left<j)
        CelerityRun(left,j,array);
    if(right>i)
        CelerityRun(i,right,array);
}
void swap(int &a,int &b)
{
    int temp = a;
    a = b;
    b = temp;
}
```
#### 快速排序
> 快速排序用到了分治的思想，将第一个数作为参照，取最后一个数与之对比，该数若大则前移若小则交换位置，然后取第一个数与交换后的参照数做比较，该数若小则后移若大则交换。交换后接着第一次前移的数继续操作，直至左边的数均比惨遭数小右边的数均比参照数大。接着以参照数的前一个数作为左边的尾以参照数右边一个数作为右边的头递归。
> 快速排序的时间是线性的即时间复杂度为O(n) 
```
#include<iostream>                    
using namespace std;
void swap(int &a,int &b);
void QuickSort(int a[],int s,int e);

int main()
{
    int i;
    int a[10];
    cout<<"为数组元素赋值:"<<endl;
    for(i=0;i<10;i++)
        cin>>a[i];
          
	QuickSort(a,0,9);
    
    for(i=0;i<10;i++){
        if(i==0)
            cout<<"排序后结果"<<endl;
        else   
            cout<<" ";
        cout<<a[i];
        if(i==9)    
            cout<<endl;
        
    }
    return 0;
}
void swap(int &a,int &b)       
{
	int temp = a;
	a = b;
	b = temp;
}
void QuickSort(int a[],int s,int e)  
{
	if(s>=e)
		return;                       
	int k=a[s];                       
	int i=s,j=e;                      
	while(i!=j){
		while(i<j&&a[j]>=k)          
			--j;	
		swap(a[i],a[j]);
		while(i<j&&a[i]<=k)
			++i;
		swap(a[i],a[j]);
	}                                
	QuickSort(a,s,i-1);
	QuickSort(a,i+1,e);
}
```
*快速排序动图*
![](http://louiszhai.github.io/docImages/sort09.gif)
---
为了方便起见所列举的排序算法都是用一个大小为10的整型数组进行测试，其他大小的也是同样道理，并且都是按从小到达的顺序来排的而从大到小则是反过来而已。
{% asset_img jieguo.jpg %}
*运行结果图*