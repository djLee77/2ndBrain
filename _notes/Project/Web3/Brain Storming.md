프론트단 - 스마트컨트랙트 생성자의 인자로 상품 금액, 판매자 지갑 주소를 입력하여 인스턴스를 생성하고, 구매 메서드를 호출하여 송금하고 상품 금액에 맞게 송금했는지 확인 후 거래 체

---
프론트엔드에서 스마트 컨트랙트의 인스턴스를 생성하길래, 생성자가 프론트엔드에서 호출되는줄 알았으나 생성자를 호출하는 것은 EVM이라는 곳에서 스마트 컨트랙트를 블록체인에 배포할 때 따로 이루어짐. 그렇기 때문에 거래 정보(판매자의 지갑주소, 상품 금액 등)을 생성자로 입력하는 방식에서 따로 메서드를 호출하여 등록하는 방식으로 변경함.

이렇게 메서드를 호출하여 변경하면 상태 변수가 실제로 변경되고 블록체인에 기록됨

![[Pasted image 20231125172823.png]]


---

판매자 지갑 주소 - 서버에서 받아옴

구매자 지갑에서 자동으로 돈 빠져나가도록 하는건 구현되어 있음

스마트 컨트랙트 인스턴스

프론트엔드측 코드
```js
// ... 기존 코드 ...

// 트랜잭션을 보내는 함수
const onClickPaymentBtn = async () => {
    // ... 기존 유효성 검사 및 설정 코드 ...

    try {
        const weiAmount = web3.utils.toWei(exchangeWonToEth(orderProduct.price * quantity).toString(), "ether");

        // 스마트 컨트랙트 인스턴스 생성
        const contract = new web3.eth.Contract(contractABI, contractAddress);

        // 판매자 정보 설정
        await contract.methods.setSellerDetails(fromAccount, weiAmount, toAddress).send({ from: fromAccount });

        // 구매 확인
        const transactionParameters = {
            from: fromAccount,
            to: contractAddress,
            value: weiAmount,
            gas: "21000", // 가스 한도
            gasPrice: web3.utils.toWei("1", "gwei"), // 가스 가격
            data: contract.methods.confirmPurchase().encodeABI()
        };

        // 메타마스크로 트랜잭션 보내기
        const result = await window.ethereum.request({
            method: "eth_sendTransaction",
            params: [transactionParameters],
        });

        console.log("영수증 : ", result);
        // 추가적인 로직 (예: 결제 정보 서버에 전송)
    } catch (error) {
        console.log(error);
        // 에러 처리...
    }
};

// ... 나머지 코드 ...

```


스마트 컨트랙트 코드
```js
pragma solidity ^0.8.0;

contract ShoppingMall {
    address public buyer;
    uint public amount;
    address payable public seller;

    function setSellerDetails(address _buyer, uint _amount, address payable _seller) public {
        buyer = _buyer;
        amount = _amount;
        seller = _seller;
    }

    function confirmPurchase() external payable {
        require(msg.sender == buyer, "Only the buyer can confirm the purchase");
        require(msg.value == amount, "Incorrect amount sent");

        seller.transfer(msg.value);
    }
}

```

---

![[Pasted image 20231125170329.png]]

대상 계정에 코드가 포함 되어 있는 경우 : 판매자 지갑 주소를 스마트 컨트랙트 내에서 정적 변수로 할당하고 스마트 컨트랙트에 직접 송금하는 케이스

현재 구현하려는 경우 : 트랜잭션에는 바이너리 데이터와 Ether가 포함될 수 있는데, 스마트 컨트랙트 인스턴스를 생성하고, 함수로 판매자의 지갑주소, 상품 금액 등 계약 정보를 등록하고, purchase 메서드로 바이너리 데이터(payload)를 받아 직접 트랜잭션에 파라미터로 입력하는 방식.

### 트랜잭션 실행 과정

1. 사용자가 트랜잭션을 승인하면, 지정된 이더가 사용자의 지갑에서 스마트 컨트랙트 주소로 전송됩니다.
2. 동시에, `data` 필드에 인코딩된 `confirmPurchase` 함수 호출이 스마트 컨트랙트에 전달됩니다.
3. 스마트 컨트랙트는 `confirmPurchase` 함수를 실행하여 내부 로직(예: 조건 검사)을 수행합니다.
4. 모든 조건이 충족되면, 스마트 컨트랙트 내부 로직에 따라 판매자의 지갑 주소로 이더가 전송됩니다.