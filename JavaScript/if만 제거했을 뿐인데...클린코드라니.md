[1] if문을 한 번 처리하는데 `O(1)` 의 시간이 걸린다고 한다. if문 자체가 많이 느린 것은 아니지만, if문을 어떻게 쓰느냐에 따라서 성능이 달라질 수 있다.

아래의 코드 스니펫을 보자.

```jsx
for (let i =0; i<m; i++){ 
   for (let j =0; j<n; j++){ 
      if (matrix[i][j]%2 != 0) count++ 
   } 
}
```

[2] 2차원 배열에서 모든 요소를 반복하고 값이 홀수이면 count 하는 코드이다. 아주 간단한 코드이며 if문을 이용해 간단하게 작성할 수 있다.  하지만 이 코드를 leetcode에서 돌렸을 때, 

- **Runtime:** **92 ms,** beats 46.58 % of javascript submissions
- **Memory Usage:** **41.8 MB,** beats 15.53 % of javascript submissions

결과가 도출되었다. 

```jsx
for (let i =0; i<m; i++){
   for (let j =0; j<n; j++){
      count += matrix[i][j]%2
   }
}
```

위의 코드는 짝수이면 0을 반환하고, 홀수이면 1을 반환하는 것을 이용해 홀수 값을 count하는 코드다. 이처럼 간단한 수학식을 이용하면 if문을 사용하지 않고 조건을 처리할 수 있는 방법도 있다.

- **Runtime:** **84 ms,** beats 77.17 % of javascript submissions.
- **Memory Usage**: **40.8 MB,** beats 40.64 % of javascript submissions.

if문 하나를 제거하는데 8ms 런타임과 메모리 1MB가 줄어드는 효과가 있었다!

[3] 또한 if문을 많이 사용하지 않고 코드를 작성할 수 있는 방법도 있다. 아래의 코드 스니펫을 보자.

```jsx
function executePayment(paymentType) {
	if(paymentType === "KAKAO_PAYMENT") {
	return "카카오 결제 처리"
	}
	else if(paymentType === "NAVER_PAYMENT") {
	return "네이버 결제 처리"
	}
	else if(paymentType === "COUPANG_PAYMENT") {
	return "쿠팡 결제 처리"
	}
	else if(paymentType === "PAYCO_PAYMENT") {
	return "페이코 결제 처리"
	}
	else if(paymentType === "APPLE_PAYMENT") {
	return "애플 결제 처리"
	}
}
```

이러한 코드를 key-value 형태의 Map을 만들어서 이용하면 if문 없이 조건을 처리할 수 있다.

```jsx
const paymentMap = {
	"KAKAO_PAYMENT" : "카카오 결제 처리",
	"COUPANG_PAYMENT" : "쿠팡 결제 처리",
	"PAYCO_PAYMENT" : "페이코 결제 처리",
	"APPLE_PAYMENT" : "애플 결제 처리",
}

function executePayment(paymentType) {
	return paymentMap[paymentType];
}

console.log(executePayment("KAKAO_PAYMENT")); // 카카오 결제 처리
```

이러한 코드의 장점은 또 하나 있다. 아래의 코드 스니펫을 보자

```jsx
function payOnKaKao() {console.log("kakao pay 처리중");
function payOnNaver() {console.log("naver pay 처리중");
function payOnCoupang() {console.log("coupang pay 처리중");
function payOnPayco() {console.log("payco pay 처리중");
function payOnApple() {console.log("apple pay 처리중");

function executePayment(paymentType) {
	if(paymentType === "KAKAO_PAYMENT") {
		payOnKakao();
	}
	else if(paymentType === "NAVER_PAYMENT") {
		sendLog();
		payOnNaver();
	}
	else if(paymentType === "COUPANG_PAYMENT") {
		sendLog();
		payOnCoupang();
	}
	else if(paymentType === "PAYCO_PAYMENT") {
		sendLog();
		payOnPayco();
	}
	else if(paymentType === "APPLE_PAYMENT") {
		sendLog();
		payOnApple();
	}
}

executePayment("KAKAO_PAYMENT"); // kakao pay 처리중
```

이 전의 if문 코드와 똑같은데 좀 더 복잡한 함수가 있다. 이러한 코드도 map을 활용하면 더 효율적으로 코드를 작성할 수 있다.

```jsx
function payOnKaKao() {console.log("kakao pay 처리중");
function payOnNaver() {console.log("naver pay 처리중");
function payOnCoupang() {console.log("coupang pay 처리중");
function payOnPayco() {console.log("payco pay 처리중");
function payOnApple() {console.log("apple pay 처리중");

const paymentMap = {
	KAKAO_PAYMENT() {
		payOnKakao();
	},
	NAVER_PAYMENT() {
		payOnKakao();
	},
	COUPANG_PAYMENT() {
		payOnKakao();
	},
	PAYCO_PAYMENT() {
		payOnKakao();
	},
	APPLE_PAYMENT() {
		payOnKakao();
	}
}

function executePayment(paymentType) {
	paymentMap[paymentType]();
}

executePayment("KAKAO_PAYMENT"); // kakao pay 처리중
```

[참고 사이트]

[1] [https://codeburst.io/if-and-only-if-2d58ef7ef027](https://codeburst.io/if-and-only-if-2d58ef7ef027)

[2]  [https://www.codeit.kr/community/threads/389](https://www.codeit.kr/community/threads/389)

[3] [`프롱트`님의 유튜브 영상](https://www.youtube.com/watch?v=toUlXhTZZ8w)