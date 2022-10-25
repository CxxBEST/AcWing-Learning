## 1. 排序与进位制

### 排序

常用排序中：

- 快排、堆排是**不稳定排序**
- 归并是**稳定排序**
- C++ sort **不稳定排序**， 可以将下标作为关键字进行***多关键字排序***从而保持稳定
- C++ stable sort 是稳定排序（基于归并排序）[std::stable_sort](https://zh.cppreference.com/w/cpp/algorithm/stable_sort)

稳定排序例题([3375. 成绩排序 ](https://www.acwing.com/problem/content/3378/))：

```c++
#include<iostream>
#include<string>
#include<algorithm>
#include<vector>

struct Student{
    std::string name;
    int socre;
};

bool operator < (const Student & s1, const Student & s2){
    return s1.socre < s2.socre;
}

bool operator > (const Student & s1, const Student & s2){
    return s1.socre > s2.socre;
}

int main(){
    int N, F;
    std::cin >> N >> F;
    std::vector<Student> S(N);
    for(int i = 0; i < N; i++)
        std::cin >> S[i].name >> S[i].socre;
    if(F)
        std::stable_sort(S.begin(), S.end());
    else
        std::stable_sort(S.begin(), S.end(), std::greater<Student>());
    for(auto it : S)
        std::cout << it.name << " " << it.socre << std::endl;
    return 0;
}
```

双关键字排序：

```c++
struct Student{
    int id;
    int socre;
};

bool operator < (const Student & s1, const Student & s2){
    if(s1.score != s2.score)
        return s1.score < s2.score;
    return s1.id < s2.id;
}
```

C++ sort的几种实现：

```c++
std::vector<ElementType> S(N);

// 默认降序, 需要重载 < 运算符
std::sort(S.begin(), S.end());

// 用标准库比较函数对象排序, 需要重载 > 运算符
std::sort(S.begin(), S.end(), std::greater<ElementType>());

// 使用自定义函数对象排序
struct {
    bool operator()(ElementType a, ElementType b) const
    {   
        return something;
    }   
} customLess;
std::sort(S.begin(), S.end(), customLess);

// 用lambda表达式排序
std::sort(s.begin(), s.end(), [](ElementType a, ElementType b) {
    return something;   
});
```

### 进位制



