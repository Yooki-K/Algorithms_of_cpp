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

    //方法五 使用fscanf按行读取，无需刷新输出流
    // FILE *fin=fopen(filename,"r");
    // FILE *fout=fopen("C.txt","w");
    // while(fscanf(fin,"%s",a)!=EOF)
    // {
    // 	fprintf(fout,"%s",a);
	// }
    // fclose(fin);
    // fclose(fout);

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
## 单词反转
```c++
void reserve_word(){
	char a[505];
	gets(a);
	char *l=a,*r=a;
	int len=strlen(a);
	a[len]=' ';
    a[len+1]=0;
	while(*r!=0){
		if(*r == ' '){
			for(char *p=r-1;p>=l;p--){//反向遍历输出单词 
				cout<<*p;
			}
			l=r+1;
            if(*(r+1)!=0){//最后一个单词后面不用输出空格 
                cout<<" ";
            }
		}
        r++;
	}
	return;
}
```
## 字符串判等
```c++
void string_is_equal(){
    char a[100]={0},b[100]={0};
    gets(a);
    gets(b);
    char *pa=a,*pb=b;
    while (*pa!='\0' || *pb!='\0')
    {
        while(*pa==' ') pa++;
        while(*pb==' ') pb++;
        if (*pa==*pb || *pa+32==*pb || *pa==*pb+32)
        {
            pa++;
            pb++;            
        }else
        {
            cout<<"no"<<endl;
            return;
        }
    }
    cout<<"yes"<<endl;
}
```
## 数字输出
```c++
int main(){
    int a;
    cout<<"请输入一个数字：";
    cin>>a;
    cout<<"输入的数字是："<<a<<endl;
    cout<<"输入的数字是：\n"<<a<<endl;
}
```
## 文件输出平均成绩
```c++
void avg_score(){
    int n=2;
    int xhs[n]={};
    char names[n][20]={};
    int scores[n][4]={};
    const char *filename="stud";
    FILE *fp=fopen(filename,"w");
    for (int i = 0; i < n; i++)
    {
        cin>>xhs[i]>>names[i]>>scores[i][0]>>scores[i][1]>>scores[i][2];
        scores[i][3]=(scores[i][0]+scores[i][1]+scores[i][2])/3;
        fprintf(fp,"%d %s %d %d %d %d\n",xhs[i],names[i],scores[i][0],scores[i][1],scores[i][2],scores[i][3]);
    }
    fclose(fp);
}
```
## 铺地毯
```c++
void blanket(){
    int n;cin>>n;
    int arr[n][4]={};
    for (int i = 0; i < n; i++)
    {
        cin>>arr[i][0]>>arr[i][1]>>arr[i][2]>>arr[i][3];
    }
    int x,y;cin>>x>>y;
    for (int i = n-1; i >=0; i--)
    {
        if (x>=arr[i][0] && x<=arr[i][0]+arr[i][2] && y>=arr[i][1] && y<=arr[i][1]+arr[i][3])
        {
            cout<<i+1<<endl;
            return;
        }
    }
    cout<<-1<<endl;
    return;
}
```
## 高精度加减法
```c++
void high_precision_add(){
    string a,b;
    cin>>a>>b;
    int flaga=1,flagb=1;
    if(a[0]=='-'){
        a.erase(0,1);
        flaga=-1;
    }
    if(b[0]=='-'){
        b.erase(0,1);
        flagb=-1;
    }
    int isABigger=a.length()>b.length()?1:(a.length()<b.length()?-1:strcmp(a.c_str(),b.c_str()));
    if((isABigger==-1 && flagb==-1)||(isABigger==1 && flaga==-1)||(flaga*flagb>0&&flaga==-1))//a大且a为负或b大且b为负或均为负数
        cout<<"-";
    if (isABigger==-1)
        swap(a,b);
    int lena=a.length();
    int lenb=b.length();
    int len=max(lena,lenb);
    int c[len+1]={0};
    int i=lena-1,j=lenb-1,k=len,jw=0;
    if(flaga*flagb>0)
        while (i>=0 || j>=0)
        {
            if(i>=0 && j>=0)
                c[k]=a[i]-'0'+b[j]-'0'+jw;
            else if(i>=0)
                c[k]=a[i]-'0'+jw;
            else if(j>=0)
                c[k]=b[j]-'0'+jw;
            jw=c[k]/10;
            c[k]%=10;
            i--;
            j--;
            k--;
        }
    else
        while (i>=0 || j>=0)
        {
            if(i>=0 && j>=0)
                c[k]=a[i]-'0'-(b[j]-'0')+jw;
            else if(i>=0)
                c[k]=a[i]-'0'+jw;
            else if(j>=0)
                c[k]=b[j]-'0'+jw;
            if (c[k]<0)
            {
                c[k]+=10;
                jw=-1;
            }else
                jw=0;
            i--;
            j--;
            k--;
        }
    c[k]+=jw; 
    i=0;
    while(c[i]==0&&i<len)
        i++;
    for (; i <= len; i++)
    {
        cout<<c[i];
    }
    cout<<endl;
}
```
## 高精度乘法
```c++
void high_precision_multi(){
    string a,b;
    cin>>a>>b;
    int flaga=1,flagb=1;
    if(a[0]=='-'){
        a.erase(0,1);
        flaga=-1;
    }
    if(b[0]=='-'){
        b.erase(0,1);
        flagb=-1;
    }
    if(flaga*flagb==-1){
        cout<<"-";
    }
    int lena=a.length();
    int lenb=b.length();
    int len=max(lena,lenb)*2;
    int c[len+1]={0};
    int i=lena-1,j=lenb-1,k=len,jw=0;
    for (; i >= 0; i--)
    {
        k=len-(lena-1-i);
        for(j=lenb-1; j >= 0; j--){
            c[k]=(a[i]-'0')*(b[j]-'0')+c[k]+jw;
            jw=c[k]/10;
            c[k]%=10;
            k--;
        }
    }
    if(jw>0){
        c[k]=jw;
    }
    i=0;
    while(c[i]==0 && i<len)
        i++;
    for (; i <= len; i++)
    {
        cout<<c[i];
    }
    cout<<endl;
}
```
## 整数去重
```c++
void int_unique(){
    int n;
    cin>>n;//输入数组大小
    int a[n];
    for (int i = 0; i < n; i++)
    {
        cin>>a[i];//输入数组元素
    }
    for (int i = 0; i < n; i++)
    {
        bool isExist=false;//判断a[i]是否在前面出现过
        for(int j=0;j<i;j++){
            if(a[i]==a[j]){
                isExist=true;
                break;
            }
        }
        if(isExist==false)//如果a[i]没在前面出现过，则输出a[i]
            cout<<a[i]<<" ";
    }
    cout<<endl;
}
```
## 数组逆序存储
```c++
void reserve_arr(){
    const int n=5;
    int a[n];
    for (int i = 0; i < n; i++)
        cin>>a[i];
    int *lp=a,*rp=a+n-1;
    while (lp<rp)
    {
        int temp=*lp;
        *lp=*rp;
        *rp=temp;
        lp++;
        rp--;
    }
    for(int i=0;i<n;i++)
        cout<<a[i]<<" ";
}
```
## 图像翻转
```c++
void romate_img(){
    int n,m;
    cin>>n>>m;
    int a[n][m];
    for(int i=0;i<n;i++){
        for(int j = 0; j < m; j++){
            cin>>a[i][j];
        }
    }
    for(int i=0;i<n;i++){
        for(int j = m-1; j >= 0; j--){
            cout<<a[j][i]<<" ";
        }
        cout<<endl;
    }
    return ;
}
```
### 约瑟夫问题（猴子）
```c++
struct node{
    int num;
    node *next;
    node(){}
    node(int n){num=n;}
};
int josephus(int n,int m){
    node *head=new node(1);
    node *p=head;
    for (int i = 2; i <= n; i++)
    {
        node *t=new node(i);
        p->next=t;
        p=p->next;
    }
    p->next=head;
    p=head;
    while (p->next!=p)
    {
        for (int i = 1; i < m-1; i++)
        {
            p=p->next;
        }
        node *t=p->next;
        p->next=t->next;
        delete t;
        p=p->next;
    }
    int res=p->num;
    delete p;
    return res;
}
```
### 学生排序
```c++
struct Student {
    string name;
    int m;
};
int cmpSty(Student x,Student y) {
    if(x.m == y.m) return x.name < y.name;
    return x.m > y.m;
}
void student_sort() {
    Student student[100];
    int n;cin>>n;
    for(int i=0;i<n;++i){
        cin>>student[i].name;
        cin>>student[i].m;
    }
    sort(student, student+n, cmpSty);
    for(int i=0;i<n;++i){
        cout<<student[i].name<<" ";
        cout<<student[i].m<<endl;
    }
}

```
### 小球下落
```c++
void ballDrop()
{
	double h;
	cin >> h;
	double s;
	for (int i=1; i<=10; i++){
		s += 1.5 * h;
		h *= 0.5; 
	} 
	cout << s - h << endl;
	cout << h << endl;
	return;
}
```
### 寻找素数对
```c++
bool isPrime(int num){
     int tmp=sqrt(num);
     for(int i=2;i<=tmp;i++)
        if(num%i==0)
          return 0;
     return 1;
}
void primePair(){
    int n;
    cin>>n;
    for(int i=5;i<=n;i+=2){
        bool flag=isPrime(i);
        if(flag&&isPrime(i-2))
                cout<<i-2<<" "<<i<<endl;
    }
    return;
}
```
### 位运算推导
```C++
2 = 0000 0010
0x33 = 0011 0011
0x55 = 0101 0101

x = (x|x<<2)&0x33 = 0000 0010
// (0000 0010|0000 1000)&0011 0011 = 0000 1010&0011 0011 = 0000 0010
x = (x|x<<1)&0x55 = 0000 0100
// (0000 0010|0000 0100)&0101 0101 = 0000 0110&0101 0101 = 0000 0100
y与x一样的，最后y = 0000 0100
z = x|y<<1
先计算y<<1 = 0000 1000
z = 0000 0100|0000 1000 = 0000 1100 = 12
```
### 机器翻译
```c++
void machine_translation(){
    int m,n,res=0,nn=0;
    cin>>m>>n;
    int arr[1001]={0};
    for(int i=0;i<n;i++){
        int t;
        cin>>t;
        if(arr[t]==0){
            ++res;
            if(nn<m){
                ++nn;
                arr[t]=nn;
            }else{
                int temp=0;
                for(int j=0;j<=1000;j++){
                    if(arr[j]>=1){
                        --arr[j];
                        ++temp;
                        if(temp==m) break;
                    }
                }
                arr[t]=m;
            }
        }
    }
    cout<<res<<endl;
    return;
}
```
