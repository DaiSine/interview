#### 部分用例未通过

1. for循环的判断条件是否需要取等，数组是从0开始还是从1开始。
2. 特殊边缘情况是否考虑到
3. 输出格式，内容是否正确
4. 箭头（ -> ）：左边必须为结构体变量指针；
   点号（ . ）：左边必须为结构体变量。

#### ⭐️C++动态分配数组

```cpp
/* 一维数组 */
int *arr = new int[lens]
for(int i = 0; i < lens; ++i) 
  	cin >> arr[i];
delete [] arr;

/* 二维数组 */
int **arr = new int *[row];
for(i=0; i<row; i++)
  arr[i] = new int[col];

```

#### 排序函数

```cpp
//sort() - int型数组排序
#include <iostream>
#include <algorithm>
using namespace std;
int main()
{
    int a[3] = {3,1,2};
    sort(a, a+3);	//参数为排序开始与结束的地址，第三个参数需自定义
    for(int i=0; i<3;++i)
        cout << a[i] << " "; //output:1 2 3 默认升序排序结果
    cout << endl;
    return 0;
}
```

```cpp
//sort() - vector 字符串容器排序
#include <string>
#include <algorithm>
#include <vector>
#include <iostream>
using namespace std;
 
bool compare(string s1, string s2)
{
		return s1.size()>s2.size();//字符串长度比较
  		//return s1>s2; 字符串直接比较
}
 
int main() {
 
	vector<string> sArray = {"123", "12A", "345", "5678", "99"};
	sort(sArray.begin(), sArray.end(), compare);
	for (auto s: sArray)
	{
		cout << s <<" "; //auto关键字遍历容器
	}
	return 0;
}
```

#### ⭐️字符串操作

```cpp
#include <string>
#include <algorithm>
#include <iostream>
using namespace std;
int main()
{
  string s;
  getline(cin, s);
  s.find("字符")//第一次出现位置
  s.rfind("字符")//最后一次出现位置
  s.insert(pos,"字符") //eg.   s.insert(11,"字符")
  s.erase(pos, len)//删除pos开始len长度的字符 len可省略直至末尾
  s.replace(begin, end, "字符")//删除加替换
  s.append("字符")//追加到末尾
    
  string s2 = s.substr(pos, n);//pos的n个字符的拷贝
  string car1 = line.substr(dash+1);//省略n 拷贝到末尾
  int c1 = count(car1.begin(),car1.end(),' ');//计空格数
}

```



#### 输入16进制，输出10进制

```cpp
#include <iostream>
using namespace std;

int main()
{
    int a;
    while(cin>>hex>>a){
    cout<<a<<endl;
    }
}
```

#### 随机整数去重排序

```cpp
#include <iostream>
using namespace std;
int main() {
    int N, n;
    while (cin >> N) {
        int a[1001] = { 0 };
        while (N--) {
            cin >> n;
            a[n] = 1;
        }
        for (int i = 0; i < 1001; i++)
            if (a[i])
                cout << i << endl;
    }
    return 0;
}
```

#### 递归

```cpp
#include <iostream>
  
using namespace std;
  
int f(int n)
{
    if(n==1) return 0;
    if(n==2) return 1;
    return f(n-2)+1;
}
  
int main()
{
    int n;
    while(cin >> n){
        if(n==0)
            break;
        cout<<f(n)<<endl;
    }
    return 0;
}

```

#### 学生成绩查询

```cpp
#include <iostream>
using namespace std;
// const int maxn=20;
// int a[maxn+1];//学生成绩组
int checkMax(int *a, int num1, int num2)
{
    int maxg = 0;
    if(num2<=num1)
    {
        int temp = num1;
        num1 = num2;
        num2 = temp;
    }
    for(int j=num1; j<=num2; j++)
    {
        if(a[j]>=maxg)
            maxg=a[j];
    }
    return maxg;

}
int main(){
    int len, n;
    while(cin >> len >> n)
    {
        int *a = new int[len + 1]; //申请动态数组的空间
        for(int i = 1; i<=len; i++)
        {
            cin>> a[i];
        }
        char op;
        int num1, num2, maxg=0;
        for(int i = 0; i<n; i++)
        {
            cin >> op >> num1 >> num2;
            if(op == 'Q')
            {
                cout << checkMax(a,num1, num2) << endl;
            }
            else
            {
                a[num1] = num2;
            }
        }
        delete[] a;
    }
    return 0;
}

```

#### 斗地主 顺子，对子，炸弹。

```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;
int main(){
    string line;
    while(getline(cin,line)){
        if(line.find("joker JOKER")!=-1)        //王炸
            cout<<"joker JOKER"<<endl;
        else{
            int dash = line.find('-');
            string car1 = line.substr(0,dash);//分成两个part比较
            string car2 = line.substr(dash+1);
            int c1 = count(car1.begin(),car1.end(),' ');
          //计算空格个数 -> 计算一组牌的长度
            int c2 = count(car2.begin(),car2.end(),' ');
            string first1 = car1.substr(0,car1.find(' '));
            //该组牌的第一个子串
            string first2 = car2.substr(0,car2.find(' '));
            string str = "345678910JQKA2jokerJOKER";
            if(c1 == c2){
                if(str.find(first1)>str.find(first2)) 
                    //个子，对子，顺子比较大小
                    cout<<car1<<endl;
                else
                    cout<<car2<<endl;
            }else                                    
                //炸弹比较大小
                if(c1 == 3)
                    cout<<car1<<endl;
                else if(c2 == 3)
                    cout<<car2<<endl;
                else
                    cout<<"ERROR"<<endl;
        }
    }
}
```

#### 字符串去重

```cpp
#include <iostream>
using namespace std;
int main() {
    char a[255],b[255];
    cin >> a;
    int k = 1, i = 0, j = 0;
    b[0] = a[0];
    while(a[i] != '\0')
    {
        for(j = 0; j < k; j++)
        {
            if(a[i] == b[j])
                break;
            if(j == (k-1))
            {
                b[k] = a[i];
                k++;
            }
        }
        i++;
    }
    cout << b << endl;
    return 0;
}
```

