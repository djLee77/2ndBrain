## 스마트 컨트랙트 구현 이미지

![[Pasted image 20231119130051.png]]
1. 생성자의 매개변수로 소유자의 propert를 입력받아 판매자의 지갑 주소를 초기화해준다.


![[Pasted image 20231119130457.png]]
2. `external` : 컨트랙트의 외부에서만 호출할 수 있는 메서드

![[Pasted image 20231119130609.png]]
3. `payable` : 이 함수가 돈을 받을 수 있다.

위 처럼 작성하면 누군가가 돈을 보냈을 때 receive 함수가 실행된다.

![[Pasted image 20231119130954.png]]
4. msg.sender : 돈을 보낸 사람의 주
5. msg.value : 보낸 금액




현재 해결해야 될 문제점 : 기본적으로 컨트랙을 배포할 때 입금 받을 지갑의 주소를 연동하여 배포하고 배포된 컨트랙 주소에 입금을 하는 방식인데, 쇼핑몰은 판매자 === 관리자가 아님으로 판매자, 판매자의 지갑 주소가 동적으로 변경이 될 수 있는 구조여야 함. 즉 판매자가 상품을 등록하거나, 판매자가 본인의 지갑을 등록할 때 컨트랙을 배포하는 과정을 자동화할 수 있어야함.

첫번째 방안 : 판매자 권한을 얻은 계정은 본인이 물건을 판매했을 때 돈을 받을 지갑을 등록할 수 있는 서비스가 있어야 함. 
그리고 지갑을 등록하면 서비스에서 컨트랙트를 생성하고 배포하는 것까지 자동화해야 함. 

그런 뒤 판매자가 상품을 등록하면 상품 정보에 판매자의 지갑 주소 대신 컨트랙트의 주소가 등록되고, 구매자에게 송금해야 될 주소 역시 판매자의 지갑 주소가 아닌 컨트랙트의 주소를 보여준다.


두번째 방안 : 
1. 여러 판매자와 지갑 주소들을 맵핑하여 한번에 관리하는 컨트랙트를 작성한다.
2. 이 컨트랙에는 판매자가 **상품을 등록할 때** 자신의 지갑 주소와 상품의 가격을 등록할 수 있는 메서드가 작성되어 있어야 한다.
3. 또한 이 컨트랙에는 구매자가 구매할때 금액을 송금할 수 있는 그리고 매개변수로 판매자의 지갑 주소를 입력 받는 메서드가 있어야 한다.
4. 새로운 판매자가 등록될 때마다 컨트랙을 재배포할 필요가 없어진다.

현재 위 스마트 컨트랙트에 대한 이해 1. 여러 판매자와 지갑 주소들을 맵핑하여 한번에 관리하는 컨트랙을 작성한다. 2. 이 컨트랙에는 판매자가 **상품을 등록할 때** 자신의 지갑 주소와 상품의 가격을 등록할 수 있는 메서드가 작성되어 있어야 한다. 3. 또한 이 컨트랙에는 구매자가 구매할때 금액을 송금할 수 있는 그리고 매개변수로 판매자의 지갑 주소를 입력 받는 메서드가 있어야 한다. 4. 새로운 판매자가 등록될 때마다 컨트랙을 재배포할 필요가 없어진다. 위 과정으로 스마트 컨트랙을 작성하고 배포 한 뒤 어플리케이션에서 판매자가 상품을 등록할 때 자신의 지갑 주소와 상품 가격을 입력하면, 스마트 컨트랙의 판매자 맵에 추가 되고, 이후에 구매자가 상품을 구매하려 할 때 스마트 컨트랙의 구매 메서드를 호출하고 매개변수로 판매자의 지갑주소와 구입 가격을 입력해주도록 구현하면 되는거지?


pragma solidity ^0.8.0;

contract ShoppingMall {
// 판매자의 주소와 가격을 매핑
mapping(address => uint) public prices;

    // 이벤트 선언
    event Purchase(address indexed buyer, address indexed seller, uint amount);
    event SellerRegistered(address indexed seller, uint price);

    // 판매자 주소와 가격을 설정하는 함수
    function registerSeller(address seller, uint price) public {
        prices[seller] = price;
        emit SellerRegistered(seller, price);
    }

    // 구매 함수
    function purchase(address seller) public payable {
        require(msg.value == prices[seller], "Incorrect amount");
        payable(seller).transfer(msg.value);
        emit Purchase(msg.sender, seller, msg.value);
    }
}
