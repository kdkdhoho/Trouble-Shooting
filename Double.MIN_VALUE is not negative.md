코딩테스트 문제를 해결하다가, 실수의 최대값을 구해야하는 알고리즘을 구현해야 하는 과정에서 `double max = Double.MIN_VALUE` 로 값을 설정하여 비교했다.

하지만 0인 값은 올바르게 비교하지 않아 디버깅과 구글링을 해보니, `Double.MIN_VALUE`는 음수가 아니기에 0은 비교하지 않고 조건문에 들어가지 않는다는 것이었다.

`Integer`의 경우는 음수라서 여태 문제없이 사용했던 것이었다.

그렇다면, `Double`은 왜 음수가 아닐까?

[Stackoverflow](https://stackoverflow.com/questions/3884793/why-is-double-min-value-in-not-negative)에 올라온 질문과 그에 대한 답변을 보면,

> The IEEE 754 format has one bit reserved for the sign and the remaining bits representing the magnitude. This means that it is "symmetrical" around origo (as opposed to the Integer values, which have one more negative value). Thus the minimum value is simply the same as the maximum value, with the sign-bit changed, so yes, -Double.MAX_VALUE is the smallest possible actual number you can represent with a double.

대충 IEEE 754 형식에는 부호를 나타내는 1bit와 크기를 나타내는 나머지 bit가 있는데, 이것은 정수값은 같다는 의미라고 해석된다. 따라서 최솟값은 최댓값에 부호만 바꾼것이라고 한다. 결국, `-Double.MAX_VALUE`가 `Double`이 실제 나타낼 수 있는 값 중 가장 작은 값이 된다.

음.. 실제로 `Double.MAX_VALUE`와 `Double.MIN_VALUE`를 출력해보자.

결과는 다음과 같이 나온다.

> Double.MAX_VALUE = 1.7976931348623157E308
> </br>Double.MIN_VALUE = 4.9E-324

실제로 둘 다 양수인 것을 확인할 수 있고, `Double.MIN_VALUE`는 실수가 나타낼 수 있는 값 중 가장 작은 값을 나타내는 것 같다.

따라서 실질적으로 `Double` 중 가장 작은 값은, `-Double.MAX_VALUE`로 나타내는 것이 맞다고 할 수 있다.
