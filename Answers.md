# c++
## 万能头文件
```c++
#include<bits/stdc++.h>
using namespace std;
```
## 斐波那契数列
```c++
//递归
int fbn(int n) {
    if (n == 1 or n == 2) return 1;
    return fbn(n - 1) + fbn(n - 2);
}
//循环
int fbn_(int k){
    int a=1,b=1,c=0;
    for (int i = 2; i < k; i++)
    {
        c=a+b;
        a=b;
        b=c;
    }
    return c;  
}
```
## 数字反转
```c++
int reverse_(int a){
    int b=0;
    while (a)
    {
        b=b*10+a%10;
        a/=10;
    }
    return b;
}
```
## 开根号嵌套
```c++
//sqrt(n+sqrt(n-1+sqrt(n-2+...+sqrt(2+sqrt(1+x)))))
double f(int x){
    if(x==1){
        return 1;
    }
    return sqrt(x+f(x-1));
}
```
## 读写文件
```c++
//读取A.txt和B.txt中的数据，将其写入C.txt中
void fopen(const char *filename){
    freopen(filename,"r",stdin);
    freopen("C.txt","w",stdout);
    // 方法一 只能读取一行
    // char a[100] = {0}; //or string a;
    // cin>>a;
    // cout<<a;
    // cin.clear();

    //方法二 使用cin.getline按行读取
    string a;
    while (getline(cin,a))
    {
        if (a.empty()) break;
        cout<<a;
    }
    cin.clear();

    // 方法三 使用scanf按行读取
    // char a[100] = {0};
    // while (scanf("%s",a)!=EOF)
    // {
    //     printf("%s",a);
    // }

    // 方法四 逐行读取
    // char a[100] = {0};
    // while (gets(a)){
    //     puts(a);
    // }
    // cin.clear();

    fclose(stdin);
    fclose(stdout);
}
void fopen_main(){
    fopen("A.txt");
    fopen("B.txt");    
}
```
## 字符串反转（指针）
```c++
void reverse_string(){
    char s[105];
    cin>>s;
    char *p = s + strlen(s);
    do
    {
        p--;
        cout<<*p;
    } while (p!=s);
    cout<<endl;
}
```
## 矩阵转置（指针）
```c++
void transpose_malloc(){
    int n,m,*p,i,j;
    scanf("%d%d",&n,&m);
    p=(int *)malloc(m*n*sizeof(int));
    //输入
    for(i=0;i<m*n;i++)
    scanf("%d",&p[i]);
    //输出
    for(i=0;i<m;i++)
    {
        for(j=0;j<n;j++)
        {
            printf("%d ",*(p+j*m+i));
        }
        printf("\n");
    }
    //释放内存
    free(p); 
}
void transpose_array(){
    int n,m,*p,i,j;
    int a[100][100]={0};
    scanf("%d%d",&n,&m);
    p=&a[0][0];
    //输入
    for(i=0;i<n;i++)
        for(j=0;j<m;j++)
        scanf("%d",(p+i*100+j));
    //输出
    for(i=0;i<m;i++)
    {
        for(j=0;j<n;j++)
        {
            printf("%d ",*(p+j*100+i));
        }
        printf("\n");
    }
}
```
## 动态随机生成数组，找最大、最小值
```c++
// 随机产生5个整数，求最大值和最小值
void max_min_1(){

    int *a=new int[5];
    int maxn=1<<31;
    int minn=1<<31-1;
    for (int i = 0; i < 5; i++)
    {
        a[i]=rand();
        if(maxn<a[i])
            maxn=a[i];
        if(minn>a[i])
            minn=a[i];
    }
    cout<<maxn<<" "<<minn<<endl;
    delete[] a;
}
void max_min_2(){

    int *a=new int[5];
    for (int i = 0; i < 5; i++)
        a[i]=rand();
    int maxn=a[0];
    int minn=a[0];
    for (int i = 1; i < 5; i++)
    {
        if(maxn<a[i])
            maxn=a[i];
        if(minn>a[i])
            minn=a[i];
    }
    cout<<maxn<<" "<<minn<<endl;
    delete[] a;
}
```
## 寻找鞍点
```c++
//寻找鞍点
void calANPoint(){
    int a[5][5];
    bool isExist=false;
    for (int i = 0; i < 5; i++)
    {
        for (int j = 0; j < 5; j++)
        {
            cin>>a[i][j];
        }
    }
    for (int i = 0; i < 5; i++)
    {
        int maxv=1<<31;
        int maxj=0;
        for (int j = 0; j < 5; j++){
            if (maxv<a[i][j])
            {
                maxv=a[i][j];
                maxj=j;
            }          
        }
        bool ismin=true;
        for(int i=0;i<5;i++){
            if (a[i][maxj]<maxv)
            {
                ismin=false;
                break;
            }
        }
        if (ismin)
        {
            isExist=true;
            cout<<i+1<<" "<<maxj+1<<" "<<maxv<<endl;
        }
    }
    if (!isExist)
    {
        cout<<"not found"<<endl;
    }
}
```
## 字符串查找
```c++
char *find(char *p,char v){
    while (*p!='\0')
    {
        if (*p==v)
        {
            return p;
        }
        p++;
    }
    return NULL;
}
```
## 第一个只出现一次的字符
```c++
void findfirstonly(){
    int a[26];//代表26个字母第一次出现的位置，-1代表没有出现过，-2代表出现多次
    char s[100];
    // memset(a,-1,sizeof(a));//数组a初始化为-1
    for (int i = 0; i < 26; i++)
    {
        a[i]=-1;
    }
    gets(s);    
    for (int i = 0; i < strlen(s); i++)
    {
        int index=s[i]-'a';//
        if(a[index]==-1) a[index]=i;// 如果第一次出现，记录位置
        else if(a[index]>=0)// 如果不是第一次出现，记为-2
        {
            a[index]=-2;
        }
    }
    int min_c;
    int min_index=-1; 
    for (int i = 0; i < 26; i++)
    {
        if (a[i]>=0) //只出现一次的字符
        {
            if(a[i]<min_index){//找到最早出现的字符
                min_index=a[i];
                min_c=i;
            }
        }
        
    }
    cout<<char('a'+min_c)<<endl;
}
``` 
## union的应用
```c++
union sts
{
	int e;
	double s;
	char d[1001];
}a[100];
void unionApply(){
	int b, p;
	string c[100];
	cin>>p>>b;
    int u=0;
    for(int i=0;i<p;i++)
    {
    	cin>>c[i];
    	if(c[i]=="DOUBLE")
    	{
    		cin>>a[i].s;
		}
		else
		{
			if(c[i]=="INT")
			{
				cin>>a[i].e;
			}
			else
			{
                getchar();//吸收空格
				gets(a[i].d);
			}
		}
	}
	int f[b];
	for(int i=0;i<b;i++)cin>>f[i];
	for(int i=0;i<b;i++)
	{
		if(c[f[i]]=="DOUBLE")
    	{
    		printf("%.2f%c",a[i].s,'\n');
		}
		else
		{
			if(c[f[i]]=="INT")
			{
				cout<<a[i].e<<'\n';
			}
			else{//!
                puts(a[i].d);
                cout<<'\n';
            } 

		}
	}
}
```
## 字符串旋转多次
```c++
/*
Youwantsomeonetohelpyou
3
1 5 100
0 3 20
2 15 60
*/
void string_rotate_1(){
    char s[100];
    gets(s);
    int n;cin>>n;
    for (int i = 0; i < n; i++)
    {
        int l,r,m;cin>>l>>r>>m;
        char temp[100];
        for (int j = 0; j < r-l+1; j++)
        {
            temp[j]=s[l+j];
        }
        for (int j = 0; j < r-l+1; j++)
        {
            s[l+(j+m)%(r-l+1)]=temp[j];
        }
    }
    puts(s);
}
void string_rotate_2()
{
    string a;
    getline(cin,a);
	string v=a;
	int b;
	cin>>b;
	int c,d,e;
	int len;
	for(int i=0;i<b;i++)
	{
		cin>>c;
		cin>>d;
		cin>>e;
		len=d-c+1;
		e%=len;//计算旋转次数 
		for(int j=c;j<=d;++j)
		{
			v[j]=a[j];
		}
		for(int i=c;i<=d;i++)
		{
			if(i+e<=d)
			{
				a[i+e]=v[i];
			}
			else
			{
				a[i+e-(d+1)+c]=v[i];
			}
		}
    }
	cout<<a;
	return;
}

```
## 交换（指针）
```c++
//指针交换
void swap_(int *p,int *q){
    int temp=*p;
    *p=*q;
    *q=temp;
}
```
## 角谷猜想
```c++
void jiaogu(){
    int a;
    cin>>a;
    while (a!=1)
    {
        if (a%2==0)
        {
            a/=2;
        }
        else
        {
            a=a*3+1;
        }
        cout<<a<<endl;
    }
    
}
```
## 哥德巴赫猜想
```c++
//是否是素数
bool isPrime(int n){
    if (n==1 or n==2) return false;
    for (int i = 2; i*i <= n; i++)
    {
        if (n%i==0) return false;
    }
    return true;
}
void goldbach(int l,int r){
    for (int i = l; i <= r; i++)
    {
        if (i%2==0)
        {
            for (int j = 3; j <= i/2; j++)
            {
                if (isPrime(j)&&isPrime(i-j))
                {
                    cout<<i<<"="<<j<<"+"<<i-j<<endl;
                    break;
                }
            }
        }
    }
}
```
