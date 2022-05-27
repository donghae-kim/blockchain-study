비트코인에 암호학은 중요하나 역설적으로 비트코인의 커뮤니케이션 및 거래 데이터는 암호화되어있지 않고 자금을 보호하기 위한 용도로 암호화 할 필요가 없다. 4장은 비트코인에서 사용되는 키,주소,지갑의 형태의 암호학을 살펴볼 것이다.

## 키와 주소

비트코인의 거래가 정당한지 혹은 누군가의 소유인지는 **디지털 키, 비트코인 주소, 디지털 서명**을 통해 알 수 있다.

- 디지털 키란 네트워크에 저장되지않고 사용자의  간단한 DB인 디지털’지갑’에서 생성하는 것으로 비트코인 네트워크와 관련성이없다.
- 비트코인 주소란 비트코인 거래에 있어서 수취인의 이름을 적는 것과 동일한 방식이다. 비트코인 주소는 공개키로부터 생성되며 공개키에 대응한다.
- 디지털 서명이란 비밀 키만 보유하고 있으면 생성될 수 있기에 비밀키의 복제본을 가지고 있는 누구나 비트코인을 관리한다. 대부분의 비트코인 거래에서는 블록체인에 포함된 유효한 디지털 서명이 필요하다.

키는 개인(비밀)키와 공개키가 한쌍으로 구성되어있다. 공개키는 은행의 계좌번호, 개인키는 비밀PIN이라고 생각하면된다. 비트코인에서 공개키와 비밀키는 지갑파일 내부에 저장되어진다.

## 공개키의 암호학과 암호화폐

소수지수함수, 타원곡선 곱셈 함수등의 수학함수는 불가역성을 보인다. 불가역성이란 한방향으로 계산하는 것은 쉽지만 반대 방향으로 계산하는 것은 실행불가능 한 것을 의미한다. 이런 수학 함수로 디지털 비밀번호와 위조가 불가능한 디지털 서명을 가능하게 한다.

비트코인은 암호학을 기반으로 타원곡선 곱셈함수를 사용한다.

비트코인에서 공개키는 비트코인을 전송받을 때 사용되며, 개인키는 전송받은 비트코인을 소비하기 위해 거래에 서명을 할 때 사용된다. 공개키와 서명을 제시하면 네트워크상에 모든 사람들이 거래를 검증하고 유효한 거래로 받아들인다.

## 개인키와 공개키

https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cda56064-4be4-492f-843b-7eb810b456c0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220527%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220527T052252Z&X-Amz-Expires=86400&X-Amz-Signature=ae38f2a3092d1f91c30e3b4c0e584905a40320810cdf3898e8fdbda547dc2b2d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject
위 사진을 통해서 알 수 있는 것은 Private key(k)를 통해 Public Key(K)가 생성되고 다시 Public Key를 통해 Bitcoin Address 가 생성된다는 것입니다. 역으로 찾아가는것은 불가합니다.

- 왜 공개키/개인키(비대칭 암호학)을 사용하는가?
    
    비트코인의 암호화는 남들이 모르도록 하는게 아니라 누구나 모든 거래에서 모든 서명을 입증하는 일이 가능한 동시에 개인키 소유주 만이 유효한 서명을 만들어내기위해 사용되어진다.
    

## 개인키(Private Key)

개인키는 돈의 소유권을 증명하고 거래를 하기위해하는 서명과 비슷한 역할을 합니다. 그렇기에 누군가에게 개인키를 공개하는 것은 비트코인의 소유를 넘겨주는 것과 같습니다.

개인키는 무작위로 추출된 숫자이며 웹사이트와는 다르게 잃어버리면 찾을 수 없습니다.

## 공개키(Public Key)

공개키는 타원곡선 곱셈 함수를 사용하여 개인키로부터 계산됩니다.  이는 K = k * G 라는 식 (k는 개인키, G는 생성포인트라는 상수, K는 식으로 부터 나오는 공개키를 의미)로 계산할 수 있습니다.  

이 함수는 역함수를 만들 수 없고 그래서 공개키로부터 개인키를 계산할 수 없기에 디지털 서명을 위조 불가능하고 안전한 것으로 만들어줍니다.

## 타원곡선 암호학

https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d13ff932-001b-4f40-811e-2d109d55d509/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220527%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220527T052241Z&X-Amz-Expires=86400&X-Amz-Signature=24e425e2facb10cfcb7f3cfe3f563a47cee701f2701f558715e26032c65b50e1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject
위 그림은 타원곡선 함수 예시입니다.

타원곡선 그래프 상에 생성포인트상수 G(ex p1)를 포함한 접선을  그어 G가 아닌 타원곡선 그래프 상에 접점(ex p2)을 구한뒤 x축 대칭(ex p3)을 시키는 과정을 반복하여 K(식으로부터 나오는 공개키)를 구하는 것입니다.

계산식 K = k * G 를 구하는 것은 위의 과정을 k번 하는 것을 의미합니다.

## 비트코인 주소

비트코인 주소는 숫자와 문자로 구성된 문자열입니다. 공개키로부터 생성된 주소는 숫자+글자 조합이며 1로 시작합니다.

이는 돈을 수령할 수 있는 대상이라고 보면 될것입니다.

https://s3.us-west-2.amazonaws.com/secure.notion-static.com/73a389b2-721e-4061-ab69-fd393a63e7f9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220527%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220527T052226Z&X-Amz-Expires=86400&X-Amz-Signature=cb0b851efa31946f363a4a526f4c4b99a509f509c6142443d0ff9f5caa1fd8eb&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject  
위의 그림은 공개키로부터 주소를 만들어내는 그림입니다.

비트코인 주소를 공개키로 부터 생성할 때는 일방 암호화 해싱을 사용합니다. 

주소 식은 A=RIPEMD160(SHA256(K)) 입니다.

A는 주소 RIPEMD,SHA256은 해싱기법, K는 공개키 입니다.

이를 통해 나온 해시값을 Base58Check로 인코딩 합니다. 사람이 읽을 수 있는 문자와 혼란이 안나게 언어를 인코딩 해줍니다. 

## Base58 인코딩

Base58이란 소문자 26개와 대문자 26개, 숫자 10개(0~9), '+'와 '/' 등과 같은 특수문자로 구성되어 있는 것 중에서 숫자 0, 대문자O, 소문자 L(l), 대문자 I (I), 와 '+', '/' 등의 부호를 쓰지 않은 것입니다. 이렇게 제외된 문자들은 서로 동일하게 보여 혼동이 올 수있는 문자들입니다.

 
https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7a4903df-e3ff-4220-9a6b-9783f40bef75/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220527%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220527T052201Z&X-Amz-Expires=86400&X-Amz-Signature=3b65cf3071a48da422ced92b6883f1d7644f4b6db5fd4f464366a5a73847a4f5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject
위 사진은 base58인코딩을 자세하게 나타낸 것입니다.

데이터(숫자)를 Base58 포맷으로 전환하기 위해서는 데이터에 버전 바이트라고 불리는 접두부를 붙여야합니다. 이는 인코딩된 데이터 유형을 쉽게 찾아볼 수 있게 합니다.

두번의 SHA256 해싱을 거쳐서 나온 32바이트의 해시값에서 첫 4바이트만을 불러와서 데이터의 끝부분에 연결합니다. 이 4byte는 checksum 역할을 합니다.

버전바이트 + data + checksum으로 구성됩니다. 이 값을 앞에서말한 Base58로 인코딩을 하면 비트코인의 주소가 만들어집니다.

## 키 포맷

개인키와 공개키는 여러 다른 포맷으로 표현될 수 있습니다. 겉으로는 달라보이지만 모두 동일한 숫자를 암호화 한 것 입니다.

## 개인키 포맷

개인키는 동일한 256비트의 숫자에 대응됩니다. 밑의 표는 공통적으로 사용되는 포맷입니다. 

| Type | Prefix | Description |
| --- | --- | --- |
| Raw | None | 32 bytes |
| Hex | None | 64 개의 16진수  |
| WIF | 5 | Base58인코딩: |
| WIF-압축형 | K or L | 위와 동일 |

| Format | Private key |
| --- | --- |
| Hex | 1e99423a4ed27608a15a2616a2b0e9e52ced330ac530edcc32c8ffc6a526aedd |
| WIF | 5J3mBbAH58CpQ3Y5RNJpUKPE62SQ5tfcvU2JpbnkeyhfsYB1Jcn |
| WIF-compressed | KxFC1jmwwCoACiCAWZ3eXa96mBM6tb3TYzGmf6YwgdGWZgawvrtJ |

위의 포맷의 예시 입니다. 서로 달라보이지만 이는 서로 다른 두개의 포맷으로 쉽게 전환될 수 있습니다.

## 공개키 포맷

공개키는 압축 공개키와 비압축 공개키가 주요 표현법입니다. 공개키는 (x,y)좌표로 타원곡선상에 위치합니다. 접두부 04로 시작하고 연속된 256비트의 x,y 숫자 2개로 표현됩니다.

비압축 포맷

- (x,y)좌표를 모두 사용하고 비압축 포맷임을 표시하기위해 앞에 0x04를 붙인다.
- 비압축 포맷의 공개키 길이 : 0x04(8비트) + x좌표(256비트) + y좌표(256비트) = 520비트 이다.

압축 포맷

- x좌표만 사용하고 압축 포맷임을 표시하기 위해 앞에 0x02(y좌표가 짝수일경우) 혹은 0x03(y좌표가 홀수일 경우)을 붙인다.
- 압축 포맷의 공개키 길이 : 0x02||0x03(8비트) + x좌표(256비트) = 264비트

## 압축 공개키

압축 공개키란 거래크기를 줄이고 비트코인 블록체인 db에 저장하는 디스크 공간을 절약하기 위해 비트코인에 도입된 것이다.

타원곡선함수를 보면 x좌표만 알면 방정식에 의해 y좌표를 계산할 수 있다. 그렇기에 이를 이용해서 압축공개키를 사용할 수 있는 것이다.

위에서 봤듯이 압축공개키와 비압축 공개키는 바이트 수가 거의 2배차이난다. 모든거래에서 50%의 크기를 절약한다면 엄청나게 많은 양이 될 것 입니다.

[![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/90336135-074f-4e58-9a75-2156f0d1d978/Untitled.png)](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/90336135-074f-4e58-9a75-2156f0d1d978/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220527%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220527T052144Z&X-Amz-Expires=86400&X-Amz-Signature=b6e5bdd4fc5196e44560e3aff3b222c729c4644547516d8e7559d7c4f6f20900&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

이는 x,y로 압축공개키와 비압축 공개키로 나뉘어지는 압축과정을 의미합니다. 

- 압축 공개키와 비압축 공개키에서 생성된 주소 두가지는 모두 유효하지만 다른 주소이다. 어떤 비트코인 주소를 검색해야할지 모를 수 있다. 그래서 압축공개키를 생성하는데 사용되었음을 보여주기 위해 다른 방식으로 구현된다. 이를 통해 주소들을 구분할 수 있다.

## 압축 개인키

잘 모르겠습니다..

## 암호화된 개인키

개인키는 비밀이 유지되어야합니다. 이 비밀을 지키기위해 종이지갑에 저장하거나 usb에 저장하지만 이 자체를 도난당하거나 분실할수도 있기에 비트코인 클라이언트는 암호화된 개인키를 위해 휴대가 가능하고 편리한 BIP-38에 의해 표준화 되었습니다.

BIP38은 개인키를 안전하게 백업 매체에 저장하고 노출될 어떤 조건에도 비밀을 유지할 수 있도록 개인키를 암호화하고 Base58로 개인키를 인코딩하는데 필요한 표준을 말합니다.

## 꾸미기 주소

꾸미기 주소란 사람이 읽을 수 있는 메세지를 포함하는 유효 비트코인 주소입니다. 

1LoveBPzzD72PUXLzCkYAtGFYmK5vYNR33 와 같은 주소에서 첫 4글자가 LOVE라는 단어로 구성된 문자를 포함하는 유효주소입니다. 이런 주소를 얻기위해 수십 억개의 개인키 후보를 생성하고 테스트해서 얻습니다.

1장에서 비트코인 모금행사를 준비하며 꾸미기 비트코인 주소를 알리기위해 1KID라는 주소를 생성하여 홍보하려는 유지니아가 있습니다.

## 꾸미기 주소 생성

만약 1KidsCharity를 얻기 위해서는 아래와 같은 시간이 걸립니다.

| Length | Pattern | Frequency | Average search time |
| --- | --- | --- | --- |
| 1 | 1K | 1 in 58 keys | < 1 milliseconds |
| 2 | 1Ki | 1 in 3,364 | 50 milliseconds |
| 3 | 1Kid | 1 in 195,000 | < 2 seconds |
| 4 | 1Kids | 1 in 11 million | 1 minute |
| 5 | 1KidsC | 1 in 656 million | 1 hour |
| 6 | 1KidsCh | 1 in 38 billion | 2 days |
| 7 | 1KidsCha | 1 in 2.2 trillion | 3–4 months |
| 8 | 1KidsChar | 1 in 128 trillion | 13–18 years |
| 9 | 1KidsChari | 1 in 7 quadrillion | 800 years |
| 10 | 1KidsCharit | 1 in 400 quadrillion | 46,000 years |
| 11 | 1KidsCharity | 1 in 23 quintillion | 2.5 million years |

이런 주소를 일반 컴퓨터로 한다면 너무 오랜 시간일 걸립니다. 그래서 주문제작 데스크톱 등의 특수하드웨어로 작업합니다.

혹은 꾸미기 풀 이라는 기능을 이용합니다. 이는 gpu를 보유한 채굴자들이 다른사람들을 위해 주소를 찾아준 대가로 비트코인을 받도록 하는 서비스입니다.

꾸미기 주소를 생성하는 방식은 무자별적으로 값을 대입해 보는 방식입니다.

## 꾸미기 주소 보안

꾸미기 주소는 보안 강화와 동시에 약화시키는데 사용할 수 있습니다.

강화되는 경우는 꾸미기 주소를 설정해놓으면 가짜주소를 위해 꾸미기 주소를 만들어야하기 떄문에 조금이나마 보안성을 강화시켜주는것입니다. 예를들어 1kids33이라는 주소가 있다면 가짜주소는 최소한 1kids33이 되어야하기 떄문입니다.

약화시키는 경우는 상대방이 비슷한 주소를 통해 고객을 속이고 가짜 주소로 지불하게끔 할 수 있기 때문입니다.

## 종이 지갑

종이 지갑은 비트코인 개인키를 종이에 인쇄한 것입니다. 이 외에도 html,외부 usb플래시드라이브의 html 등이 종이지갑이라고 할 수 있습니다. 이로써 온라인 체제에 저장되지 않고 종이위에만 존재하는 종이지갑을 생성할 수 있습니다.
https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1f901068-5390-4d63-b4cf-2d304ec4013e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220527%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220527T052114Z&X-Amz-Expires=86400&X-Amz-Signature=356dc79a93a3fd6173611909a9860da476ff46e5fa40e02ad4e628b8e19c596c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject
