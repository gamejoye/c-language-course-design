# c-language-course-design
c的18周课设啦
   ######"1". 如果开始输入回车的话，最先打印的是第10页码😯（虽然我也有懵杯））
#include<stdio.h>
#include<time.h>
#include<stdlib.h>
int a[1000];//定义全局变量保存生成的1000个随机数
int max(int x);//求该页码最大数
int min(int x);//求该页码最小数
float average(int x);//求平均数

void main()
{
    int i,j,k,l=0,max1,min1;
    float average1;
    char ch;
    srand(time(NULL));//重新播种
    for(i=0,j=0 ; j<1000 ; j++)
        a[j]=rand()%1000+1;//生成1000个随机数
    while(1)
    {
        printf("press any key to continue...\n");
        ch=getchar();
        if(ch=='\n')
            i++;//判断是回车的话页码加1
        if(ch!='\n')
            for(i=1 ; i<10 ; i++)
                if(i==(ch-48))
                    break;//输入要查询的页码
        system("clear");
        if(i<0||i>=10)
            i=1;//要查询页码若错误，则返回第一页码
        for(k=(i-1)*100; k<i*100; k++)
        {
            printf("%-3d ",a[k]);
            l++;
            if(l==10)
            {
                printf("\n");
                l=0;
            }
        }//打印页码
        max1=max(i);
        min1=min(i);
        average1=average(i);
        printf("max=%3d\n",max1);
        printf("min=%3d\n",min1);
        printf("average=%.2f\n",average1);
    }
}
int max(int x)
{
    int max=0,k;
    for(k=(x-1)*100; k<x*100; k++)
        if(a[k]>=max)
            max=a[k];
    return max;
}
int min(int x)
{
    int min=1001,k;
    for(k=(x-1)*100; k<x*100; k++)
        if(a[k]<=min)
            min=a[k];
    return min;
}
float average(int x)
{
    int k;
    float sum=0;
    for(k=(x-1)*100; k<x*100; k++)
        sum=sum+a[k];
    sum=sum/100;
    return sum;
}


  #####"2".
  #include<stdio.h>
void main()
{
    float y,x1,x,sum=0;
    scanf("%f",&x1);
    for(x=1;x<=2;x=x+x1)
    {
        y=1/(x*x+4*x)*x1;
        sum=sum+y;
    }
    printf("%f\n",sum);
}

  #####"3"
#include<stdio.h>
#include<math.h>
void main()
{
    float a,b,c,y,y1,r,i=100000;
    float x=0;
    scanf("%f%f%f",&a,&b,&c);
    scanf("%f",&r);
    while(i--)
    {
        y1=2*a*x-b;
        if(fabs(r*y1)<=0.0000000000001)
        break;
        x=x-r*y1;
    }
    x=-x;
    y=a*x*x+b*x+c;
    printf("%f %f",x,y);
}
