namespace
----------
##### namespace란
namespace 자체는 별게 아니다..
그냥 이름 그대로 어떤 공간에 이름을 붙여주는게 namespace이다.
namespace가 왜 필요할까?
이름이 겹치는 식별자(변수, 함수, ...)가 같은 범위 내에 있을 경우 충돌이 발생하는데, 이를 막기 위해 사용하는 것이 namespace이다.

A.h라는 헤더와 B.h라는 헤더가 있다고 생각해보자.
나는 A에 있는 method1()이라는 함수를 사용하기 위해 다음과 같은 코드를 작성했다.

'''
#include "A.h"
#include "B.h"

int main() {

  method1();
  
  return 0;
}
'''

그런데 공교롭게도 B.h헤더에도 이름이 동일한 method1() 이 존재했다.
이럴 경우 함수의 이름이 충돌하기 때문에 오류가 발생하게 된다.
이 때 namespace 개념을 사용하면 이런 충돌을 방지할 수 있다.

'''
//A.h 헤더 안에 namespace A 생성
namespace A {
  method1() {
    //실행할 내용
  }
}
'''

'''
//B.h 헤더 안에 namespace B 생성
namespace B {
  method1() {
    //실행할 내용
  }
}
'''

이제 범위지정연산자(::)를 통해 method1()을 오류 없이 사용할 수 있다.

'''
#include "A.h"
#include "B.h"

int main() {

  A::method1(); // A헤더의 method1() 호출
  
  return 0;
}
'''


##### using namespace std;에 대하여
C++ 코드에서 using namespace std;라는 구문을 작성해놓은 것을 자주 볼 수 있다.
그러나 이것은 bad practice로 간주되기도 한다.
왜냐하면 std의 함수와 이름이 겹치는 함수를 사용하게 되면 나의 의도와 다른 결과가 나올 수 있기 때문이다.
짧은 코드를 작성할 때에는 괜찮지만 코드가 길어지면 오류가 발생할 수 있으니 조심하자.
'''
using namespace std::cout;
'''
이렇게 사용하고 싶은 것을 구체적으로 적거나
'''
std::cout<<"Hello World!"<<endl;
'''
이렇게 범위 지정 연산자를 적어주도록 하자.
