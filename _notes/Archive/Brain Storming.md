프론트단 - 스마트컨트랙트 생성자의 인자로 상품 금액, 판매자 지갑 주소를 입력하여 인스턴스를 생성하고, 구매 메서드를 호출하여 송금하고 상품 금액에 맞게 송금했는지 확인 후 거래 체

---

판매자 지갑 주소 - 서버에서 받아옴

구매자 지갑에서 자동으로 돈 빠져나가도록 하는건 구현되어 있음

스마트 컨트랙트 인스턴

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