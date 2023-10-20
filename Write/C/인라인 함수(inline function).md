C++에서 함수의 호출은 꽤 복잡한 과정을 거칩니다.

이때, 함수를 실행하는 시간이 오래 걸린다면, 함수를 호출하는데 걸리는 시간은 전혀 문제가 되지 않습니다. 하지만 함수의 실행 시간이 매우 짧다면, 함수 호출에 걸리는 시간도 부담이 될 수 있습니다.

C++에서는 이러한 경우에 사용할 수 있는 인라인 함수(inline function)이라는 것을 제공합니다. 인라인 함수는 일반적인 함수의 호출 과정을 거치지 않고, 함수의 모든 코드를 호출된 자리에 바로 삽입하는 방식의 함수입니다.

함수를 호출하는 데 걸리는 시간은 절약되나, 함수 호출과정으로 생기는 여러 이점을 포기하게 됩니다. 따라서 코드가 매우 적은 함수만을 인라인 함수로 선언하는 것이 좋습니다.

### 예제

#### 사용 코드
```c
inline int Sub(int x, int y) { return x - y; }

inline void Print(int x) { cout << "계산 결과는 " << x << "입니다."; }

int main(void)

{

    int num1 = 5, num2 = 3;

    int result;

    result = Sub(num1, num2);

    Print(result);

    return 0;

}
```

#### 실제 시행 방식

```c
int main(void)

{

    int num1 = 5, num2 = 3;

    int result;

    {

        int x = num1, y = num2;

        result = x - y;

    }

    {

        int x = result;

        cout << "계산 결과는 " << x << "입니다.";

    }

    return 0;

}
```

작성자 : Subin