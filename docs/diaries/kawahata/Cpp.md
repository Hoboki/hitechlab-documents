20220610
# sstreamの使い方

```cpp
#include <iostream>
#include <vector>
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

# a人をb人のグループに分けると何グループできる？
`(a + b - 1) / b`


>[名前](url)

___

__Qustion__
