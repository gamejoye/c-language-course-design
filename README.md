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
        y1=2*a*x+b;
        if(fabs(r*y1)<=0.0000000000001)
        break;
        x=x-r*y1;
    }
    y=a*x*x+b*x+c;
    printf("%f %f",x,y);
}

  #####"4" k-means(虽然但是好像不是很好康的样子)
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#include<math.h>
int x[10],y[10],xe[65]={0},ye[65]={0};
int point[40][80];
void randonkk(int a)
{
    int i=0,j=0,x0,y0;
    srand(time(NULL));
    for(i=0;i<a;i++)
    {
        x0=rand()%40;
        y0=rand()%80;
        xe[i]=x0;
        ye[i]=y0;
    }
}
void getpoint(int k,int a)
{
    int i,j,m,l;
	srand(time(NULL));
    for(i=0;i<k;i++)
    {
        m=rand()%a;
        x[i]=xe[m];
        y[i]=ye[m];
    }
}
float os(int A,int B,int C,int D)
{
    float s;
    s=sqrt(pow(A-C,2)+pow(B-D,2));
    return s;
}
void main()
{
    int i,j,k,a,m[10]={0},ji1,ji2,ji,t=1000,sum[10],sun[10];
    float min=1001;
    srand(time(NULL));
    a=rand()%51+15;
    randonkk(a);
    scanf("%d",&k);
    getpoint(k,a);
    while(t--)
    {
    for(j=0;j<a;j++)
    {
        for(i=0;i<k;i++)
        {
        if(min>os(x[i],y[i],xe[j],ye[j]))
        {
            min=os(x[i],y[i],xe[j],ye[j]);
            ji1=xe[j];
            ji2=ye[j];
            ji=i;
        }
        }
        point[ji1][ji2]=ji+1;
        m[ji]++;
        sum[ji]=sum[ji]+ji1;
        sun[ji]=sun[ji]+ji2;
        min=1001;
    }
    for(j=0;j<k;j++)
    {
        x[j]=(sum[j]+x[j])/(m[j]+1)+0.5;
        y[j]=(sun[j]+y[j])/(m[j]+1)+0.5;
        sum[j]=0;
        sun[j]=0;
        m[j]=0;
    }
    }
    for(i=0;i<40;i++)
    {
    for(j=0;j<80;j++)
    {
    if(point[i][j]!=0)
    printf("%d",point[i][j]);
    else
    printf(" ");
    }
    printf("\n");
    }
}
  #####"5"(进制转换)（做的我烦呐）
#include<stdio.h>
#include<math.h>
void transX2X(char num1[],int,int,char num2[]);
void main()
{
    int n,m,i;
    char num1[256]={'\0'},num2[256]={'\0'};
    scanf("%s%d%d",num1,&n,&m);
    transX2X(num1,n,m,num2);
    for(i=0;num2[i]!='\0';i++);//得到转化完成后的字符串的最后一个字符序数
    for(i=i-1;i>=0;i--)
    printf("%c",num2[i]);//需要逆序输出（随便举个简单例子就很明了啦）
}
void transX2X(char num1[],int n,int m,char num2[])
{
    int i,d,j;
    int sum=0;
    for(i=0;num1[i]!='\0';i++);
    for(j=0,i=i-1;i>=0;i--,j++)
    {
        if(num1[i]>'9')
        num1[i]=num1[i]-39;//用来判断10进制以上的需要转换的数
        sum=sum+(num1[i]-48)*pow(n,j);
    }
    for(i=0;;i++)
    {
        d=sum%m;
        if(d==10)
        d=97;
        if(d==11)
        d=98;
        if(d==12)
        d=99;
        if(d==13)
        d=100;
        if(d==14)
        d=101;
        if(d==15)
        d=102;
        if(d<97)
        d=d+48;
        num2[i]=d;
        sum=sum/m;
        if(sum==0)
        break;
    }
}

 #####"6"排序（冒泡，快速，直接插入，选择排序）
//冒泡排序
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#define N 10
void main()
{
    int a[N];
    int i,j=0,k,t;
    srand(time(NULL));
    for(i=0;i<N;i++)
    a[i]=rand()%51+1;
    printf("冒泡排序前的数组:");
    for(i=0;i<N-1;i++)
    printf("%d ",a[i]);
    printf("%d\n",a[i]);
    while(1)
    {
    for(i=0;i<N-1;i++)
    {
    if(a[i]>a[i+1])
    {
        t=a[i];
        a[i]=a[i+1];
        a[i+1]=t;
        j++;
    }
    }
    if(j==0)
    break;
    j=0;
    }
    printf("冒泡排序后的数组:");
    for(i=0;i<N-1;i++)
    printf("%d ",a[i]);
    printf("%d\n",a[i]);
}

  #####"7"
  #include<stdio.h>
#include<math.h> 
void main()
{
    int n,k,i,j,a[10][10],m,l,d;
    int b[10][9];
    scanf("%d,%d",&n,&k);
    for(i=0;i<n;i++)
    for(j=0;j<n;j++)
    scanf("%d",&a[i][j]);
    for(i=0;i<n;i++)
    {
        for(l=0;l<k;)
        {
        for(j=0;j<n;j++)
        {
            if(d<a[i][j]&&a[i][j]!=0)
            {
                d=a[i][j];
                m=j;
            }
        }
        b[i][l]=m+1;
        a[i][m]=0;
        l++;
        d=0;
        m=0;
        }
    }
    for(i=0;i<n;i++)
    {
    for(j=0;j<k;j++)
    printf("%d ",b[i][j]);
    printf("\n");
    }
}

  #####"8"，可恶，我承认我是five
  #include<stdio.h>
#include<math.h>
void paixu(float a[],int n);
void main()
{
    float a[60],b[60],c[60],count;
    int i,j,k,n,max1=0,min1=1000,max2=0,min2=1000,max3=0,min3=1000,v;
    float pass[3],average1,average2,average3,sum1=0,sum2=0,sum3=0;
    float paverage[60];
    scanf("%d",&n);
    for(i=0; i<n; i++)
    {
        scanf("%f%f%f",&a[i],&b[i],&c[i]);
        if(a[i]<=min1)//求各科最大和最小
            min1=a[i];
        if(a[i]>=max1)
            max1=a[i];
        if(b[i]<=min2)
            min2=b[i];
        if(b[i]>=max2)
            max2=b[i];
        if(c[i]<=min3)
            min3=c[i];
        if(c[i]>=max3)
            max3=c[i];
        paverage[i]=(a[i]+b[i]+c[i])/3;//计算个人平均分
        sum1=sum1+a[i];
        sum2=sum2+b[i];
        sum3=sum3+c[i];
    }
    average1=sum1/n;//计算程序设计平均分
    average2=sum2/n;//计算英语平均分
    average3=sum3/n;//计算数学平均分
    for(i=0; i<n; i++)
        printf("第%d个同学程序设计:%.2f 英语:%.2f 数学:%.2f 个人平均:%.2f\n",i+1,a[i],b[i],c[i],paverage[i]);
    printf("程序设计平均分:%.2f 程序设计最高分:%d 程序设计最低分:%d\n",average1,max1,min1);
    printf("英语平均分:%.2f 英语最高分:%d 英语最低分:%d\n",average2,max2,min2);
    printf("数学平均分:%.2f 数学最高分:%d 数学最低分:%d\n",average3,max3,min3);
    for(count=0,i=0; i<n; i++)
        if(a[i]>=60)
            count++;
    pass[0]=count/n;
    for(count=0,i=0; i<n; i++)
        if(b[i]>=60)
            count++;
    pass[1]=count/n;
    for(count=0,i=0; i<n; i++)
        if(c[i]>=60)
            count++;
    pass[2]=count/n;
    printf("程序设计及格率:%f 英语及格率:%f 数学及格率:%f\n",pass[0],pass[1],pass[2]);
    paixu(paverage,n);
    for(i=0; i<n; i++)
        printf("第%d名:%.0f\n",i+1,paverage[i]+1);
}
void paixu(float a[],int n)
{
    int i=0,j,k,m;
    float b[60],d=0;
    while(1)
    {
        for(j=0; j<n; j++)
        {
            if(a[j]>=d&&a[j]>=0)
            {
                d=a[j];
                m=j;
            }
        }
        a[m]=-1;
        b[i]=m;
        d=0;
        i++;
        if(i==n)
            break;
    }
    for(i=0; i<n; i++)
        a[i]=b[i];
}

  #####"9"(深化部分)（推箱子啦）(并没有很完美)
//难度其实也只有2，3，4，5可以选啦
#include<stdio.h>
#include<math.h>
#include<stdlib.h>
#include<time.h>
#define n 20
void obstacles(char a[][n],int j);
void newsites(char ch);
int date1=1; //箱子纵坐标
int date2=1; //箱子横坐标
int datep1=0; //人纵坐标
int datep2=0; //人横坐标
int count=0;//步数
char a[n][n]= {'\0'};
void main()
{
    int c,d,i,j;
    char ch;
    srand(time(NULL));
    c=rand()%(n-1);
    a[c][n-1]=']';//生成出口
    a[datep1][datep2]='P';//生成人
    a[date1][date2]='O';//生成箱子
    printf("请输入难度关卡:\n");
    scanf("%d",&d);
    getchar();
    obstacles(a,d);//生成障碍物
    for(i=0; i<n-1; i++)
    {
        for(j=0; j<n; j++)
        {
                if(a[i][j]!='\0')
                printf("%c",a[i][j]);
                else
                printf(" ");
        }
        printf("\n");
    }
    printf("%d\n",count);//生成初始画面
    while(1)
    {
        ch=getchar();
        count++;
        getchar();
        system("clear");
        newsites(ch);
        //判断游戏失败或成功
        if(date2==n-1&&date1==c)
        {
            printf("sucessed!\n");
            break;
        }
        if((date1==-1||date1==n-1)&&date1!=c)
        {
            printf("falied!\n");
            break;
        }
        //否则则继续进行下去
        for(i=0; i<n-1; i++)
        {
            for(j=0; j<n; j++)
            {
                if(a[i][j]!='\0')
                    printf("%c",a[i][j]);
                else
                    printf(" ");
            }
            printf("\n");
        }
        printf("%d\n",count);//生成画面
    }
}
void obstacles(char a[][n],int d)
{
    int j=3,k,l;
    srand(time(NULL));
    while(d--)
    {
        l=rand()%n;
            for(k=0; k<n; k++)
                if(k!=l)
                    a[k][j]='|';
        j=j+3;
    }
}
void newsites(char ch)
{
    int old1=date1,old2=date2;
    int oldp1=datep1,oldp2=datep2;
    if(ch=='a')
    {
        if(a[datep1][datep2-1]=='|')//如果小人往左走是墙壁，计数不变
        count--;
        else
        {
        if(datep2==date2+1&&datep1==date1)//如果小人在箱子的右边
        {
            if(a[date1][date2-1]!='|')//如果箱子的左边不是是墙壁
            {
                date2--;
                datep2--;
            }
            else//如果小人箱子的左边是墙壁，计数不变
            count--;
        }
        else
        datep2--;
        }
    }
    if(ch=='d')
    {
        if(a[datep1][datep2+1]=='|')//如果小人往右走是墙壁，计数不变
        count--;
        else
        {
        if(datep2==date2-1&&datep1==date1)//如果小人在箱子的左边
        {
            if(a[date1][date2+1]!='|')//如果箱子的右边不是是墙壁
            {
                date2++;
                datep2++;
            }
            else//如果小人箱子的右边是墙壁，计数不变
            count--;
        }
        else
        datep2++;
        }
    }
    if(ch=='s')
    {
        if(datep1==date1-1&&datep2==date2)//如果小人在箱子的上边，箱子往下一个单位
            date1++;
        datep1++;//人往下一个单位
    }
    if(ch=='w')
    {
        if(datep1==date1+1&&datep2==date2)//如果小人在箱子的下边，箱子往上一个单位
            date1--;
        datep1--;//人往上一个单位
    }
    a[old1][old2]='\0';
    a[oldp1][oldp2]='\0';//清空原来的人和箱子
    a[datep1][datep2]='P';
    a[date1][date2]='O';//将新的位置赋予人和箱子
}
