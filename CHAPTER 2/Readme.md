# 2장: 비트코인의 작동원리

2장에서는 비트코인 시스템 내에서 진행되는 거래 과정에서 상위 단계에 있는 비트코인을 추적해서 거래 한 건이 분산화된 합의라는 비트코인 메커니즘에 의해 ‘신뢰’를 얻고 승인을 받은 후 거래 내역 전부가 담긴 분산 장부인 블록체인에 최종적으로 기록되는 과정을 살펴볼 것이다.

## **커피 한잔 구매하기**

1장에 등장했던 앨리스는 비트코인으로 밥의 커피 가게에서 커피를 한잔 구매할 계획이다. 밥의 카페는 최근 들어 비트코인을 결제 수단으로 받기 시작했다. 밥은 “1달러 50센트나 15밀리비트로 지불하시면 됩니다”라고 말한다. 밥의 pos시스템이 지불요청이 들어 있는 특수 QR코드를 자동적으로 생성한다.

https://s3.us-west-2.amazonaws.com/secure.notion-static.com/df28347f-a2ff-4a79-b87a-1984aeaa75b3/image3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220526%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220526T124217Z&X-Amz-Expires=86400&X-Amz-Signature=f093845b40aa7b686d6ad5e7ab666eccb3a6bab86d95f9cc89b5c821c5621a82&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22image3.png%22&x-id=GetObject

단순히 목적지의 비트코인 주소만 들어있는 QR코드와는 달리 지불요청은 QR코드로 인코딩되어 있는 URL로 목적지 주소, 지불 금액, ‘밥스 카페’ 등과 같이 지불과 관련된 기본적인 설명을 담고 있다.

QR코드를 찍으면 나오는 정보:

bitcoin:1GdK9UzpHBzqzX2A9JFP3Di4weBwqgmoQA?amount=0.015&label=Bob%27s%20Cafe&message=Purchase%20at%20Bob%27s%20Cafe

앨리스가 스마트폰을 사용해 QR코드를 스캔하고, 밥스 카페로 btc 지불을 승인한다면 몇 초 후 거래가 완료된다.

이제 앨리스의 지갑이 어떻게 거래를 성사시키는지 / 해당 거래가 어떻게 네트워크상으로 전파되는지 / 해당 거래가 어떤 방법으로 검증되는지 알아볼 것이다.

## **거래 입력값과 출력값**

거래는 복식부기 장부에 나오는 대변과 차변으로 구성된다.

차변: 하나 이상의 ‘입력값’ / 비트코인 계좌에서 빠져나가는 값

대변: 하나 이상의 ‘출력값’ / 비트코인 계좌로 들어오는 값

거래 수수료: 공개 장부에 거래를 포함시킨 채굴자가 수거하는 소액의 지불금

입력값 = 출력값 + 거래 수수료

https://s3.us-west-2.amazonaws.com/secure.notion-static.com/368e6298-5a9f-44a2-b87b-b303c8fef400/image4.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220526%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220526T124250Z&X-Amz-Expires=86400&X-Amz-Signature=df2e4ed9a06e98779a5258c83ef97fe61a752e442b68bf485991228174a2930f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22image4.png%22&x-id=GetObject

송금되는 비트코인의 금액(입력값) 각각에 대한 소유권을 소유주의 디지털 서명을 통해 증명하는 과정이 거래에 포함되며 누구든지 독립적으로 거래를 검증할 수 있다. 비트코인 용어로 ‘소비(Spending)’이라 함은 이전 거래에서 송금되었던 돈이 비트코인 주소에 의해 확인된 새로운 소유주에게로 전송되는 거래에 서명을 함으로써 이루어지는 작업을 말한다.

## **거래 유형**

[![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c310dda2-8328-4dba-91e0-77cf2554253c/image5.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c310dda2-8328-4dba-91e0-77cf2554253c/image5.png)](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c310dda2-8328-4dba-91e0-77cf2554253c/image5.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220526%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220526T124301Z&X-Amz-Expires=86400&X-Amz-Signature=6149840d1d2d3e48ab7e7a4c9c90a1d4184a8486b725571ca1ae11c2e393721f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22image5.png%22&x-id=GetObject)

가장 흔하게 볼 수 있는 거래 유형은 하나의 주소에서 다른 주소로 단일 거래가 이루어지는 형태다. 이 경우 원 소유주에게 돌려줘야 하는 ‘잔액’이 존재할 수 있으며, 이 때 그림 2-5와 같이 하나의 입력값과 두 개의 출력값이 발생한다.

[![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/93d85100-8786-4fe5-b8d3-02342b0c5547/image6.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/93d85100-8786-4fe5-b8d3-02342b0c5547/image6.png)](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/93d85100-8786-4fe5-b8d3-02342b0c5547/image6.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220526%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220526T124313Z&X-Amz-Expires=86400&X-Amz-Signature=1b2c3ff56a62f6f37683c0fdfd542deaa4e732f977d61ae187f19b4df3a998e4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22image6.png%22&x-id=GetObject)

또 다른 유형으로는 여러 개의 입력값을 하나의 출력값으로 합치는 거래다. 이 형태는 실제로 동전과 단위가 작은 지폐가 많이 있는 경우 큰 단위의 지폐 한장으로 교환되는 행위와 동일하다.

[![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/78fadc6e-f24d-486f-afb0-3eafff083cfb/image7.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/78fadc6e-f24d-486f-afb0-3eafff083cfb/image7.png)](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/78fadc6e-f24d-486f-afb0-3eafff083cfb/image7.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220526%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220526T124328Z&X-Amz-Expires=86400&X-Amz-Signature=92370226ec891d5e3e63c2be3821f16d6ec08de595c0d28d44d53c404a64dd07&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22image7.png%22&x-id=GetObject)

마지막으로, 하나의 입력값을 여러 명의 수취인에게 줄 수 있는 여러 개의 출력값으로 배분하는 형태다.

## **앨리스의 지갑이 어떻게 거래를 성사키는지**

1. 올바른 입력값 얻기
- 풀 노드 클라이언트를 사용하는 비트코인 지갑:
    
    블록체인 상에 있는 모든 거래에서 실제로 발생한 소비되지 않은 출력값을 보유하고 있기 때문에 지갑에서 거래 입력값을 생성할 수 있을 뿐 아니라 향후 거래에서 신속하게 검증할 수 있다.
    
- 라이트웨이트 클라이언트를 사용하는 비트코인 지갑:
    
    API를 이용하거나 API호출을 이용하고 있는 풀 노드에 해당 정보를 검색해달라고 요청하여 소비되지 않은 출력값을 얻을 수 있다.
    
1. 출력값 생성하기

거래 출력값은 해당 가치에 대한 예상 지출을 생성하는 스크립트의 형태로 만들어진다. 즉, 앨리스의 거래 출력값에는 ‘이 출력값은 밥의 공개키에 대응하는 키를 이용해 서명을 하는 누구에게나 지불 가능하다.’라는 의미가 담겨 있는 스크립트를 포함한다.

이 거래의 경우, 출력값이 하나 더 존재한다. 앨리스의 잔액에 대한 지불은 밥에 대한 지불과 동일한 거래 내에서 이루어지며 앨리스의 지갑에서 출력값으로 생성된다. 앨리스의 지갑에서는 그녀가 보유한 돈이 두가지 거래로 쪼개진다. 하나는 밥에게 송금되는 거래이고 하나는 그녀가 잔액을 수신하는 거래다.

## **해당 거래가 어떻게 네트워크상으로 전파되는지**

비트코인 네트워크는 P2P네트워크로 각각의 비트코인 고객이 여러 다른 비트코인 고객들에게 접속함으로써 네트워크에 참여하게 된다. 비트코인 네트워크의 목적은 거래내역과 블록을 참여자 전원에게 전파하는 것이다.

비트코인 노드: 비트코인 프로토콜을 이용해서 비트코인 네트워크에 참여하는 서버, 데스크톱 어플리케이션, 지갑 등의 모든 시스템

앨리스의 비트코인 지갑에서 유선, 와이파이, 휴대폰 등 어떠한 종류의 연결만 되어 있으면 모든 비트코인 노드들에 새로운 거래를 전송할 수 있다.

플러딩: 비트코인 노드가 이전에는 없던 유효한 거래를 전송받으면 즉시 연결되어 있는 다른 노드로 해당 거래를 전달하는 전파 기술

플러딩을 통해 거래를 P2P네트워크를 통해 급속도로 전파되고 몇 초만에 비트코인 네트워크 대부분에게 도달하게 된다.

## **해당 거래가 어떤 방법으로 검증되는지**

앨리스의 거래가 비트코인 네트워크 상에 전파가 된 후 이 거래가 채굴이라는 과정을 거쳐 블록이 포함되면 비로소 블록체인의 일부가 된다. 채굴 과정은 비트코인 시스템 내에서 두 가지 목적을 가지고 있다.

1. 채굴 노드는 비트코인의 합의 규칙을 참조해서 모든 거래를 입증한다. 따라서 채굴 과정에서 유효하지 않거나 형식이 잘못된 거래가 거부됨으로써 비트코인 거래에 대한 신뢰도가 생긴다.
2. 채굴 과정은 돈을 새로 발행하는 중앙은행처럼 각 블록 내에서 새 비트코인을 생성한다. 한 블록당 생성되는 비트코인의 양은 제한되어 있고 시간이 지나면서 줄어든다.

앨리스의 거래가 네트워크에서 선택되어 미검증 거래들로 이루어진 채굴 풀에 포함될 때, 채굴 소프트웨어로 입증되면 앨리스의 거래는 채굴 풀이 생성한 후보 블록이라는 이름의 새로운 블록에 게시된다. 이 채굴에 참여하고 있던 모든 채굴기들이 즉시 이 후보 블록에 대한 작업 증명 계산을 한다. 어떤 채굴기가 해당 블록에 대한 솔루션을 찾아내면 네트워크상에 게시된다. 다른 채굴기가 승리한 블록을 검증하면, 채굴에 실패했다는 사실을 알게 된 나머지 채굴기들도 새 블록을 채굴하는 과정을 시작한다. 블록이 완성되면 거래에 대한 ‘승인’이 일어난 것으로 간주된다.

[![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/63968967-9ad7-4f03-9e5f-7e1dcc5dfc68/image8.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/63968967-9ad7-4f03-9e5f-7e1dcc5dfc68/image8.png)](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/63968967-9ad7-4f03-9e5f-7e1dcc5dfc68/image8.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220526%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220526T124341Z&X-Amz-Expires=86400&X-Amz-Signature=b9e5faa117b18fa803d02805babcdba4abbef1c2971ce7302367d742346f81d8&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22image8.png%22&x-id=GetObject)

새 블록들이 이전 블록 위에 세워지면서 블록체인에 연산이 추가되며 거래들의 신뢰도가 높아진다. 시간이 흐름에 따라 블록의 ‘높이’가 높아지면 각 블록과 체인의 계산 난이도가 전반적으로 올라가고 앨리스의 거래가 들어 있는 블록 이후에 채굴된 블록들은 더 강한 강도로 앨리스의 거래를 보증한다.
