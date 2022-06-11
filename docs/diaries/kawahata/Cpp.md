2022年

6月

# sstreamの使い方

```cpp
#include <iostream>
#include <sstream>
using namespace std;

int main(void) {
  string str;
  getline(cin, str);
  istringstream ss(str);
  
  getline(cin, str);
  ss.str(str); //再代入
  ss.clear(stringstream::goodbit); //クリアしないと使えない
}
```

## a人をb人のグループに分けると何グループできる？
`(a + b - 1) / b`

# 配列の検索

```cpp
vector<string> vec = { "hello", "world" };

auto res = find(vec.begin(), vec.end(), "world");
if (res != vec.end()) {
  cout << *result << endl;
}
```

# 2次元配列の検索

```cpp
vector<vector<string>> vec = { {"hello", "world"}, {"docker", "compose"} };

auto res = find_if(vec.begin(), vec.end(),
  [&](const auto& row) {return row.at(0) == "docker" && row.at(1) == "compose";}
);
if (res != vec.end()) {
  //
}
```
