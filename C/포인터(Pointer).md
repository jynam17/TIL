## 포인터 변수를 인덱싱?


CS50 강의에서 문자열이 `char *` 타입이라는 것을 설명하기 위해 아래와 같은 코드를 보여줬다.
```c
char *s = "hello";
printf("%p\n", &s[0]);
printf("%p\n", s);
```
위 코드를 실행하면 아래와 같은 출력이 나온다.
```
0x42add1
0x42add1
```
이를 통해 알 수 있는 사실은 `s`는 "helle"라는 문자열의 첫번째 문자의 메모리 주소라는 것이다.

그런데 나는 `s[0]`라는 문법에 의문이 들었다.

> s는 포인터 변수인데 `[]`으로 인덱싱이 가능한 것인가? 이는 배열만 가능한 것이 아니었나?

결론부터 말하자면 사실 c언어에서 배열은 배열 내 첫 번째 원소의 주소이다. <br />
따라서 인덱싱은 배열만 가능한 것이 아니라, 포인터 변수에 인덱싱이 가능하니 배열도 가능한 것이다.

배열 `a`가 있다면 `a[0]`는 `a`의 첫 번째 원소이며, `a`는 `a[0]`의 주소인 셈이다.

아래는 같은 `"hello"`라는 문자열을 3가지  변수에 저장한 것이다.
```c
char *s = "hello";
printf("%p\n", &s[0]);
printf("%p\n\n", s);

char charArr[5] = {'h', 'e', 'l', 'l', 'o'};
printf("%p\n", &charArr[0]);
printf("%p\n\n", charArr);

char string[5] = "hello";
printf("%p\n", &string[0]);
printf("%p\n\n", string);
```

아래는 다양한 케이스로 실험해본 코드이다.
```c
int n = 50;
int *p = &n;
printf("%p\n", &p[1]);
printf("%p\n\n", p);

char *s = "hello";
printf("%p\n", &s[0]);
printf("%p\n\n", s);

char charArr[5] = {'h', 'e', 'l', 'l', 'o'};
printf("%p\n", &charArr[0]);
printf("%p\n\n", charArr);

int intArr[5] = {0, 1, 2, 3, 4};
printf("%p\n", &intArr[0]);
printf("%p\n", intArr);
```
출력
```
0x7ffdbb25288c //  &p[1] => int는 4바이트이므로 0x7ffdbb252888의 4바이트 뒤가 출력된 것이다.
0x7ffdbb252888 

0x42aeb1
0x42aeb1

0x7ffdbb252873
0x7ffdbb252873

0x7ffdbb252850
0x7ffdbb252850
```

TMI지만 이 결론에 쉽게 접근할 수 있었던 이유는 c++ 프로그래밍 수업을 들었기 때문인데, 그 당시에는 왜 배열이 포인터인 것인지 이해를 못하고 그 사실 자체만 받아들였었다. <br />
이 강의 덕분에 확실히 이해하고 갈 수 있어서 좋다!
