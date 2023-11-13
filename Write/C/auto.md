auto는 자동 형식 추론을 지원하는 키워드이다.

'auto'를 사용하면 컴파일러가 변수의 자료형을 자동으로 추론하게 되어, 코드를 간결하게 만들 수 있다.

'auto'를 사용할 때 주의할 점은, 초기화 식에서 추론될 수 있는 자료형이 명확해야한다는 것이다.

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
	// int 형식을 갖는 변수
	auto x = 5;

	// double 형식을 갖는 변수
	auto y = 3.14;

	// vector의 형식을 갖는 변수
	vector<int> numbers = {1, 2, 3, 4, 5};
	auto iter = numbers.begin();

	//반복자 형식을 갖는 변수
	for(auto it = numbers.begin(); it != numbers.end(); ++i) {
		cout << *it << " ";
	}

	return 0;
}
```