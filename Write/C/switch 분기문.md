switch 분기문은 if와 else if에 비해 여러 조건을 손쉽게 처리할 수 있다.

case와 함께 사용하여 변수의 값이 case에 지정한 값과 동일하면 해당 코드를 실행한다. 
(case에는 조건식이나 변수를 지정할 수 없음.)
어떤 case에도 해당되지 않을 시 default(생략가능)의 코드를 실행한다.

case를 작성할 때에는 그 부분의 마지막에서 break로 중단해  주어야 해당 case만 실행시킬 수 있다. 그렇게 하지 않는다면 그 다음에 있는 코드들이 계속 실행된다.

case 안에서도 변수 선언을 할 수 있다. 이것은 case안에서만 사용할 수 있다.

실수 자료형은 사용할 수 없다.

#예제 
표준 입력으로 문자 'f', 'c', 'p' 중 하나가 입력됩니다. 입력된 문자가 'f'라면 "환타", 'c'라면 "콜라", 'p'라면 "포카리스웨트"를 출력하고, 아무 문자에도 해당되지 않으면 "판매하지 않는 메뉴"를 출력하는 프로그램을 만드세요.

```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int main()
{
    char memu;

    scanf("%c", &memu);

    switch (memu)
    {
    case 'f':
            printf("환타");
            break;

    case 'c':
            printf("콜라");
            break;

    case 'p':
            printf("포카리스웨트");
            break;

    default:
            printf("판매하지 않는 메뉴");
    }

    return 0;
}
```

---

작성자 hyisu

