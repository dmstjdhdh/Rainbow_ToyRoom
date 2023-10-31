do while 반복문은 초기식이 반복문 바깥에 있다. 또한 do 로 시작하여 중괄호 안에 반복할 코드와 변화식이 같이 들어가며 중괄호가 끝나는 부분에 조건식을 지정한다.

```c
초기식
do 
{
    반복할 코드
    변화식
} while (조건식);
```
이런 방식이다.

do while은 처음 한 번은 실행해야 하고 그 이후에 조건에 따라 반복해야 하는 코드를 간단하게 표현할 수 있다.

while 반복문은 조건식이 만족하지 않으면 반복하지 않는데, do while 반복문은 최소 한 번은 실행하는 반복문이다.

    예제

표준 입력으로 정수가 입력됩니다(입력 값의 범위는 0~1000). 다음 소스 코드를 완성하여 0부터 입력된 숫자까지의 합이 출력되게 만드세요.

```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int main()
{
    unsigned int num1;
    unsigned int sum = 0;

    scanf("%d", &num1);

    unsigned int i = 0;
    do
    {
        sum += i;
        i++;

    } while (i <= num1);

        printf("%d\n", sum);

        return 0;
}
```
---
작성자 - hyisu