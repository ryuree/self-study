# 11주차
## Promise
- 비동기 처리에 사용(비동기 : 특정코드의 실행이 완료 되기 전에 다음코드 실행)
- 서버에서 받아온 데이터 표시할 때 사용
- 데이터를 보내올때 받아오기도 전에 데이터를 요청하기 때문에 문제를 해결하기 위해 사용
```js

//Promise 선언
var _promise = function (param) {

	return new Promise(function (resolve, reject) {

		// 비동기를 표현하기 위해 setTimeout 함수를 사용 
		window.setTimeout(function () {

			// 파라메터가 참이면, 
			if (param) {

				// 해결됨 
				resolve("해결 완료");
			}

			// 파라메터가 거짓이면, 
			else {

				// 실패 
				reject(Error("실패!!"));
			}
		}, 3000);
	});
};

//Promise 실행
_promise(true)
.then(function (text) {
	// 성공시
	console.log(text);
}, function (error) {
	// 실패시 
	console.error(error);
});

```
### Promise 상태
- Pending(대기) : 로직 완료 전
- Fulfilled(이행) : 비동기 처리 완료 후 결과값 반환 === 완료
- Rejected(실패) : 비동기 처리 실패 또는 오류 발생
- Settled : 처리의 유무의 상관 없이 결론이 난 상태 

```js

function getData() {
  return new Promise(function (resolve, reject) {
    $.get('url 주소/products/1', function (response) {
      if (response) {
        resolve(response);
      }
      reject(new Error("Request is failed"));
    });
  });
}

// Fulfilled 또는 Rejected의 결과 값 출력
getData().then(function (data) {
  console.log(data); // response 값 출력
}).catch(function (err) {
  console.error(err); // Error 출력
});

```
- then()으로 여러개의 Promise 연결 가능

## Async & Await
- Async는 Promise가 없으면 의미가 없음
- Await 는 Promise를 받아 처리하는 키워드 이고, 사용하려면 Async가 선언되어야함
- Await는 Async바로 안에서 선언되어야함, Async함수안에 다른 일반 함수 안에 Await사용하면 안됨
- 에러 발생시 아무일도 일어나지 않기때문에 try Catch문으로 감싸서 명시적으로 처리해 주어야함
- Async안에 여러개의 Await가 있을경우 순서대로 처리 됨


[참고]
- https://joshua1988.github.io/web-development/javascript/promise-for-beginners/
- https://programmingsummaries.tistory.com/325