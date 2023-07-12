**AST가 궁금해진 이유? 자바스크립트 컴파일 과정에서 갑자기 AST..추상구조트리라는 개념이 나와서 궁금증이 생겼다.** :flushed:

#### AST란?
* 추상구조트리로 간단히 말하면 프로그래밍 언어의 문법에 따라 소스코드 구조를 표시한 것이다.
* 어휘분석 및 구문분석의 두단계가 코드를 기반으로 AST를 만드는데 주요 역할을 담당하고 있다.
  * 첫번째 단계 = 어휘분석기 = Scanner: 정의된 규칙을 사용하여 문자 스트림을 사용하여 읽고 이를 토큰으로 결합한다. 즉, 전체 토큰 목록으로 분할된다.
  * 두번째 단계 = 구문분석기 = Parser: 토큰 목록을 가져와서 언어 구문을 검증하고 이를 트리 구조로 변환한다.

```
// AST로 변환하기 전의 함수
function square(n) {
  return n * n
}

// AST로 변환하면..
{
  "type": "Program",
  "start": 0,
  "end": 36,
  "loc": {
    "start": {
      "line": 1,
      "column": 0
    },
    "end": {
      "line": 3,
      "column": 1
    }
  },
  "range": [0, 36],
  "errors": [],
  "comments": [],
  "sourceType": "module",
  "body": [
    {
      "type": "FunctionDeclaration",
      "start": 0,
      "end": 36,
      "loc": {
        "start": {
          "line": 1,
          "column": 0
        },
        "end": {
          "line": 3,
          "column": 1
        }
      },
// ... 이하 코드 생량
}
```
