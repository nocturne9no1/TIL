# Blockchain Explained

- [원문 링크](https://www.investopedia.com/terms/b/blockchain.asp)

## 블록체인이란 무엇인가?

블록체인은 컴퓨터 네트워크 노드들에 나뉘어 분산된 데이터베이스 혹은 원장(ledger, 장부)이다. 블록체인은 암호화폐 시스템의 보안 유지와 탈중앙화된 트랜잭션 기록을 위한 중요한 역할로 잘 알려져 있지만, 사용이 암호화폐에 국한되지는 않는다. 블록체인은 어떤 산업에서든 변경불가능한 데이터를 만드는데 사용될 수 있다.

블럭을 바꿀 수 있는 방법이 없기 때문에, 유저나 프로그램이 데이터를 삽입하는 포인트에만 신뢰가 필요하게 된다. 이런 측면은 비용을 증대시키고 실수를 만들수도 있는 회계 감사나 다른 사람들과 같은 서드 파티들의 신뢰 필요성을 감소시킨다.

2009년 피트코인이 소개된 이래로, 블록체인은 다양한 암호화폐, 탈중앙화 금융(DeFi) 어플리케이션, 대체 불가능한 토큰(NFTs), 스마트 컨트랙트 등을 통해 폭발적으로 성장했다.

> 핵심
>
> - 블록체인은 정보를 저장하는 방식이 일반적인 데이터베이스와 다른 공유 데이터베이스의 한 종류이다. 블록체인은 암호학을 통해 서로 연결된 블록에 데이터를 저장한다.
> - 블록체인에는 서로다른 다양한 종류의 정보가 저장될 수 있다. 하지만 가장 많이 트랜잭션을 위해 가장 많이 사용되는 분야는 장부이다.
> - 비트코인의 경우, 블록체인은 탈중앙화되어 하나의 사람이나 그룹이 컨트롤 할 수 없다. 대신, 모든 사용자가 집단적으로 통제권을 유지한다.
> - 탈중앙화된 블록체인은 변경 불가능하다. 이것이 시사하는 바는 데이터를 되돌릴 수 없다는 것이다. 비트코인에서, 트랜잭션들은 영구적으로 기록되고 누구에게나 보여진다.

## 블록체인은 어떻게 동작하는가?

당신은 스프레드시트나 데이터베이스에 친숙할 것이다. 블록체인은 저것들과 비슷하다. 왜냐하면 블록체인은 정보가 들어보고 저장되는 데이터베이스이기 때문이다. 하지만 전통적인 데이터베이스나 스프레드시트와 블록체인의 중요한 차이점은 데이터를 구조화하고 접근하는 방식이다.

블록체인은 스크립트라고 불리는 프로그램으로 구성되어 있다. 이 프로그램은 기존 데이터베이스에서의 작업을 수행한다. 즉, 정보를 입력하고 접근하는 것과 어딘가에 저장하고 보관하는 것이다. 블록체인은 분산되어 있다. 이는 여러개의 복제본들이 많은 기계들에 저장되고 모두 유효하게 동일(match)함을 의미한다.

블록체인은 트랜잭션 정보와 그것이 블럭에 들어오는 것을 모은다. 마치 스프레드시트의 셀이 정보를 담고 있는 것처럼 말이다. 이것이 가득 찼을 때, 정보는 해시라 불리는 16진법 수로 바꿔주는 암호화 알고리즘 속에 들어간다.

그런 다음 해시는 다음 블록 헤더에 입력되고 블록의 다른정보로 암호화된다. 이러한 블록들의 연속된 생성은 함께 엮이게(chained)된다.

### 트랜잭션 프로세스

트랜잭션은 그들이 위치한 블록체인에 의존하는 특정한 프로세스를 따른다. 예를 들어 비트코인 블록체인에서는 네가 만약 너의 암호화폐 지갑(블록체인을 위한 인터페이스를 제공하는)을 사용한 트랜잭션을 시작하면, 이벤트들이 순차적으로 시작된다.

비트코인에서, 너의 트랜잭션은 메모리 풀로 보내진다. 이곳에서는 트랜잭션이 채굴자다 검증자가 고를 때까지 저장되고 queued된다. 트랜잭션이 블럭으로 들어오고 블럭이 트랜잭션들로 채워졌을 때, 블록은 암호화 알고리즘을 사용하여 닫히고 암호화된다. 다음으로 채굴은 다시 시작된다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/27c1f799-d745-4a57-b880-e0c7e03ec250/b89906fb-38a1-4908-953c-9fd8dd6cd0dc/Untitled.png)

1. 새로운 트랜잭션이 들어옴
2. 트랜잭션은 전세계에 뿌려진 peer-to-peer 컴퓨터 네트워크에 보내짐
3. 이 컴퓨터들의 네트워크는 트랜잭션 유효성 검증을 위해 방정식을 해결함
4. 정당한 트랜잭션으로 확인되었을 때, 트랜잭션들은 무리를 이뤄 블록에 들어감
5. 이 블록들은 함께 chained되어 영구적인 모든 트랜잭션들의 긴 history를 생성함
6. 트랜잭션이 완료됨

전체 네트워크는 해시 문제를 “풀기”위해 동시에 작동한다. 각 해시는 한번 사용한 숫자(number used once)의 줄임말인 “nonce”를 제외하고 랜덤 해시를 생성한다.

모든 채굴자는 무작위로 생성된 해시인 nonce 0 부터 시작한다. 만약 숫자가 목표 해시값 이하가 아니라면, nonce 값에 1이 추가된다. 그리고 새로운 블록 해시가 추가된다. 이 행위는 채굴자가 유효한 해시를 생성할 때 까지 지속되며 유효 해시 생성시 보상을 받게 된다.

> **재밌는 사실** 특정 값까지 랜덤 해시를 생성하는 것은 많이 들어 봤을 “작업 증명(proof-of-work)”이다. 이는 채굴자가 작업을 완수했다는 것을 “증명”하는 것이다. 이러한 채굴이 해시 검증을 위해 차지하는 작업 양은  왜 비트코인 네트워크가 그렇게 많은 계산 능력과 에너지를 소비하는지 알려준다.

블록 하나가 닫힐 때, 트랜잭션은 완료된다. 그러나 그 블록이 다른 다섯개의 블록이 검증되기 전에는 확인되지 않은 것으로 간주된다. 확인 작업은 블록당 평균 10분 미만이기 때문에 완료하는 데 약 1시간 정도 걸린다. (거래 있는 첫 블록과 이어지는 다섯 개 블록 = 총 6개 블록, 6 * 10 = 60분)

모든 블록체인이 이 프로세스를 따르는 건 아니다. 가령 이더리움 네트워크는 블록을 검증하기 위해 이더리움을 스테이크한 모든 유저중 하나를 랜덤으로 고른다. 이 검증자들은 네트워크에 의해 확인된다. 이런 방식은 비트코인 프로세스보다 훨씬 빠르고 에너지를 덜 소모한다.

## 블록체인 탈중앙화

블록체인은 다양한 지역에서 데이터베이스 내의 데이터를 몇몇 네트워크 노드(컴퓨터나 블록체인 소프트웨어를 위해 가동하는 장치 등)로 뿌리는 것을 허용한다. 이를 통해 데이터의 중복이 발생하지만, 데이터의 신뢰성은 올라간다. 예를 들어, 누군가 데이터베이스의 한 인스턴스의 기록을 바꾸려 시도할 때, 다른 노드들은 이런 일을 방지할 수 있다. 이런 방식으로, 네트워크 내 어떤 단일 노드도 네트워크 내 보유된 정보를 변경할 수 없다.

이런 분배와 작업이 수행되었다는 암호화된 증거로 인해, 정보와 history는 되돌릴 수 없다. 이런 기록은 암호화폐와 같은 거래 목록이 될 수도 있지만, 블록체인이 법적 계약이나 국가 신분증, 또는 기업의 재고와 같은 다양한 다른 정보를 보유하는 것 또한 가능하다.

## 블록체인 투명성

비트코인 블록체인의 탈중앙화된 환경으로 인해, 모든 트랜잭션을 트랜잭션 실황을 보는 [블록체인 익스플로러](https://www.blockchain.com/explorer?utm_campaign=dcomnav_explorer)를 사용하거나 개인 노드를 가진 사람들이 투명하고 볼 수 있다. 새 블록들로 하여금 업데이트된 체인의 각 복사본을 가진 각 노드들은 확인되고 추가된다. 이는 네가 원한다면, 비트코인이 어디로 가든 추적할 수 있음을 의미한다.

예를 들어, 교환들은 과거 해킹되곤 했다. 이는 막대한 양의 암호화폐 손실을 야기했다. 해커가 익명이라 하더라도, 지갑 주소는 블록체인에서 공개이기 때문에 쉽게 추적할 수 있다.

물론 비트코인 블록체인에 저장된 기록들은 암호화되어 있다. 이는 주소가 할당된 사람만 자신의 신원을 밝힐 수 있다는 것을 의미한다. 결과적으로, 블록체인 사용자들은 투명성을 지키며 익명성을 유지할 수 있다.

## 블록체인은 안전한가?(보안)

블록체인 기술은 탈중앙화된 보안과 신뢰를 다방면에서 달성한다. 새로운 블록들은 항상 선형이며 시간 발생순으로 저장된다. 그들은 항상 블록체인의 “끝”에 추가된다. 블록이 블록체인의 끝에 추가된 뒤, 이전 블록들은 바뀔 수 없다.

어느 한 데이터의 변경은 블록의 해시를 변경하게 된다. 각 블록은 이전 블록의 해시를 가지고 있기에, 한 곳에서의 변경은 뒤따르는 블록들도 변경하게 된다. 네트워크는 해시가 일치하지 않기에 대체된 블록을 거절한다.

> 꿀잼 사실 모든 블록체인이 100% 안전하다고 할 수는 없다. 블록체인은 코드를 사용해 보안 레벨을 만드는 분산된 장부다. 만약 코드 취약점이 있다면, 이용당할 수 있다.

예를 들어, 상상해보라, 해커가 블록체인 네트워크 노드를 운영하면서 블록체인을 변경하고 다른 모든 사람들로부터 암호화폐를 훔치려 한다. 만약 그들이 그들의 복사본을 바꾼다면, 다른 노드에 자신의 복사본이 유효하다고 확신시켜야 한다.

해커는 이를 위해 네트워크에서 가장 많은 수를 컨트롤할 필요가 있고 이를 적절한 순간에 넣어야 한다. 이는 51% 공격으로 알려져 있다. 왜냐하면 너는 이를 시도하려면 네트워크에서 50% 이상을 컨트롤해야 하기 때문이다.

타이밍은 이런 방식의 공격에서 전부이다. 해커가 어떤 액션을 취할 때, 네트워크는 변경하려는 블록을 지나쳐 이동했을 가능성이 크다. 이는 비트코인 네트워크 해시 속도가 매우 빠르기 때문이다.

## 비트코인 vs 블록체인

블록체인 기술은 문서 타임스탬프를 변조할 수 없는 시스템을 구현하기 원했던 두 연구자인 Stuart Haber와 W. Scott Stornetta에 의해 1991년 처음 제안되었다. 하지만 거의 20년이 지난 2009년 1월 비트코인의 출시와 함께 블록체인이 최초의 실제 응용 프로그램을 갖게 되었다.

비트코인 프로토콜은 블록체인 위에 만들어졌다. 비트코인의 익명 개발자인 사토시 나카모토는 디지털 화폐를 소개하는 연구 논문에서 “신뢰할 수 있는 제 3자가 없는 완전한 P2P(Peer-to-Peer)인 새로운 전자 현금 시스템”이라고 언급했다.

이해를 위한 핵심은 비트코인이 장부나 기타 당사자 간 거래를 투명하게 기로하기 위한 수단으로 블록체인을 활용한다는 것이다.

### 블록체인

블록체인은 변경 불가능한 기록을 위해 사용된다. 이는 트랜잭션, 선거에서 투표, 제품 재고, 국가 신분증, 가정에 대한 증서, 그 밖에도 여러가지를 위한 형태가 될 수 있다.

현재, 수만개의 프로젝트가 블록체인을 단순히 트랜잭션을 기록하는 것을 넘어서 사회를 도울 수 있는 다양한 방식을 실행하기 위해 연구하고 있다. 예를 들어, 민주주의 선거에서 비밀 투표를 위해

블록체인 불변성의 특성은 부정 투표가 훨씬 어려워진다는 것을 의미한다. 예를 들어, 투표 시스템은 각 국가의 시민들이 단일 암호화폐나 토큰을 발행받을 수 있도록 작동할 수 있다.

각 후보는 특정 지갑 주소로 받을 것이며 투표자들은 그들의 토큰이나 암호 화폐를 그들이 뽑고 싶은 후보에게 전달할 수 있을 것이다. 블록체인의 특성인 투명성과 추적 가능성은 사람이 표를 세는 것과 물리적 투표를 조작할 수 있는 능력을 없앨 것이다.

## 블록체인 vs 은행

블록체인은 금융 분야에 지장을 주는 힘으로 예견되어 왔다. 특히 지불과 뱅킹 기능에서 말이다. 그러나, 은행과 탈중앙화된 블록체인은 몹시 다르다.

은행과 블록체인의 차이를 알기 위해, 뱅킹 시스템과 비트코인의 블록체인 수행을 비교해보자.

| 항목                                                         | 은행                                                         | 비트코인             |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------------------- |
| 오픈 시간                                                    | 보통 은행은 평일 오전 9시부터 오후 5시까지 연다. 몇몇 은행은 주말에도 열지만 시간 제약이 있다. 모든 은행은 은행 휴일에는 쉰다. | 24/7, 365일 연중무휴 |
| 거래 수수료                                                  | * 카드 결제                                                  |                      |
| 이 수수료는 카드에 따라 다르다. 사용자가 직접 지불하지 않는다. 수수료는 상점에서 결제 처리자가 지불하며 보통 거래당 부과된다. 이 수수료의 효과로 인해 이따금 상품 및 서비스의 비용이 상승할 수도 있다. |                                                              |                      |

- 수표 은행에 따라 1달러에서 30달러 사이의 비용이 발생할 수 있다.
- ACH ACH 송금은 외부 계좌로 전송할 때 최대 3달러의 비용이 발생할 수 있다.
- 무선 국내선 송금은 25달러까지 발생할 수 있다. 국제선 송금은 45달러까지 발생할 수 있다.  | 비트코인은 채굴자와 사용자에 의해 결정되는 다양한 결제 수수료가 있다. 이 수수료는 0달러에서 50달러까지의 범위를 가지지만 사용자는 얼만큼의 수수료를 지불할 지에 대해 결정할 수 있다. 이는 사용자가 너무 낮은 수수료를 설정하면 결제가 진행되지 않을 수도 있음을 의미한다. | | 결제 속도 | * 카드 결제 24-48 시간이 걸린다.
- 체크 카드 24-72시간이 걸린다
- ACH 24-48 시간
- 무선 국제가 아니라면 24시간 이내
- 은행 송급은 보통 휴일이나 주말에 이뤄지지 않는다. | 비트코인 결제는 15분 내로 이뤄지며 네트워크 혼잡에 따라 한시간 이상 걸릴 수도 있다. | | 고객에 대해 알기 | 은행 계좌와 다른 은행 상품은 “Know Your Customer”(KYC) 절차를 요구한다. 이는 은행이 계좌를 열기 위해 고객의 신원을 기록해야하는 합법적인 요구를 의미한다. | 그 어떤 신원 없이도 블록체인 네트워크에 누구나 어떤 것이든 참여할 수 있다. 이론적으로, 인공지능 또한 참여할 수 있다. | | 송금 용이성 | 정부 발행 신분증, 은행 계좌, 그리고 핸드폰은 전자 송금의 최소 요구 조건이다. | 인터넷 연결과 핸드폰만이 최소 요구 사항이다. | | 개인정보 | 은행 계좌 정보는 은행 사설 서버에 저장되고 고객에 의해 보유된다. 은행 계좌 개인 정보는 은행이 서버에 저장된 정보를 보호하고 유저가 정보를 보호하기 위해 제한되어 있다. 만약 은행 서버가 제대로 동작하지 못한다면, 개인 계좌또한 그러하다. | 비트코인은 유저의 소망대로 private해질 수 있다. 모든 비트코인은 추적 가능하지만 익명으로 구매되었다면 비트코인이 누구의 소유인지 알 수가 없다. 비트코인이 KYC 교환위에 구매되었다면 그 비트코인은 직접적으로 KYC 교환 계좌의 홀더에게 묶인다. | | 보안 | 사용자가 안전한 비밀번호와 이중 인증과 같은 견고한 인터넷 보안 조치를 실행한다 가정할 때, 은행 계좌 정보는 고객 계좌 정보를 포함하는 은행의 서버 만큼만 안전하다. | 비트코인 네트워크가 커질 수록 보안성도 증대한다. 비트코인 홀더가 자신의 비트코인에 대해 갖는 보안 수준은 전적으로 그들에게 달려있기에, 사람들은 더 많은 양의 비트코인 또는 장기간 보유하고자 하는 양을 위해 콜드 스토리지를 사용하는 것이 더 좋다. | | 승인된 트랜잭션 | 은행은 다양한 이유에서 결제를 거절할 권리를 가진다. 은행은 또한 계좌 동결의 권리또한 가진다. 만약 너의 은행이 특이한 장소나 특이한 상품에 대한 구매를 알게된다면 거부할 수 있다. | 비트코인 네트워크는 비트코인이 어떻게 쓰이든지 상관하지 않는다. 사용자는 그들이 적합하다고 생각되는 곳에 비트코인을 사용할 수 있지만, 그들이 사는 지역의 법도는 따라야 한다. | | 계좌 압수 | KYC 법에 따라, 정부는 쉽게 사람들의 은행 계좌를 추적하고 다양한 이유로 그들의 계좌를 압수할 수 있다. | 만약 비트코인이 익명으로 사용되었을 때, 정부는 그걸 추적하고 압수하는데 힘든 시간을 보낼 것이다. |

## 블록체인은 어떻게 쓰이나?

우리가 알고 있듯이, 비트코인 블록체인의 블록들은 트랜잭션 데이터를 저장한다. 오늘날, 23,000개 이상의 암호화폐 시스팀이 블록체인에서 동작하고 있다. 하지만 블록체인은 다른 유형의 거래에 대한 데이터를 저장하는 신뢰할 수 있는 방법임이 밝혀졌다.

몇몇 회사는 블록체인 경험을 선사한다. (월마트, 화이자, AIG, 지멘스 등등). 예를 들어 IBM은 음식 제품이 그들 지역에 도달할 때 까지의 여정을 음식 신뢰 블록체인로 만들었다.

왜 이렇게 할까? 음식 산업은 수없이 많은 대장균, 살모넬라, 리스테리아의 발생을 목도해왔다. 어떤 경우에는, 위험 물질들이 식품에 우연히 유입되기도 한다. 과거에는, 이러한 발생의 원인이나 질병의 원인을 사람들이 먹는 것으로부터 찾는데 몇 주가 걸렸다.

블록체인의 사용은 식품의 원산지에서부터 출발지, 경유지, 배송지까지의 경로를 추적할 수 있다. 뿐만 아니라, 이 회사들은 이제 식품 접촉 가능성이 있는 모든 것들을 볼 수 있으므로 문제 파악이 훨씬 빨라 생명을 구할 수도 있다. 이것은 실제 블록체인의 한 예시지만, 다른 많은 형태의 블록체인 구현이 존재한다.

### 은행과 금융

아마 그 어떤 산업도 그 사업 운영에 블록체인 도입을 통해 얻을 수 있는 이득이 은행보다 크지는 않을 것이다. 금융 산업은 비즈니스 시간에만 운영된다. 보통 일주일 중 5일이다. 이는 네가 만약 금요일 오후 6시에 예금하고 싶은데 월요일 아침까지 기다려야 함을 의미한다.

심지어 네가 만약 너의 예금을 비즈니스 시간에 한다해도, 결제는 1일에서 3일이 걸릴 것이다. 반면 블록체인은 잠들지 않는다.

블록체인을 은행애 도입함으로써, 소비자는 그들의 결제가 몇분, 혹은 몇초내로 진행됨을 볼 수 있을 것이다. 이 시간은 블록체인에 블록이 추가되는 시간이다. 이는 휴일이나 평일, 주말 상관없이 진행된다. 블록체인과 함께, 은행은 또한 기관 사이의 환전을 빠르고 보안성있게 진행할 수 있다. 관련 금액의 크기를 고려할 때, 심지어 돈이 송금되는 며칠 동안에도 은행들은 상당한 비용과 위험을 부담할 수 있다.

주식 거래자들의 결제 및 청산 과정은 최대 3일(국제 거래의 경우 더 김)이 소요될 수 있는데, 이는 해당 기간 동안 자금과 주식이 동결되는 것을 의미한다. 블록체인은 그 시간을 대폭 줄여줄 수 있다.

### 통화

블록체인은 비트코인과 같은 암호화폐의 기반을 형성한다. 미국 달러는 연방준비제도에 의해 통제된다. 이런 중앙 권한 제도 하에, 사용자의 데이터와 통화는 기술적으로 그들의 은행 또는 정부의 생각에 따라 결정된다. 사용자의 은행이 해킹 당하면 고객의 개인 정보다 위험에 처하게 된다.

만약 고객의 은행이 파산하거나 불안정한 정보에 사는 고객이라면, 그들의 화폐 가치에는 리스크가 있다. 2008년, 몇몇 실패한 은행이 드러났다. 이들은 비트코인이 고려되고 개발되는 원인이 되었다.

> 중요 블록체인은 불안정한 통화나 금융 기반이 있는 나라에 더 안정적인 통화와 금융 시스템을 줄 수 있다. 그들은 더 많은 어플리케이션과 더 넓은 네트워크에 접근할 수 있다.

블록체인은 컴퓨터 네트워크를 통해 운영을 확장함으로써, 비트코인을 비롯한 암호화폐를 중앙기관 없이 운영할 수 있도록 하여, 이를 통해 위험뿐 아니라 처리 및 거래 수수료 절감또한 도모할 수 있다.

암호화폐 지갑을 저축 계좌나 결제 수단으로 사용하는 것은 국가 신분증이 없는 사람들에게 특히 중요하다. 일부 국가는 전쟁으로인해 피폐해졌거나 정부가 실제 신원 확인을 진행하기위한 인프라가 부족할 수도 있다. 이런 국가의 시민들은 저축 계좌나 중개 계좌에 접근할 수 없을 수 있으며, 이에 따라 재산을 안전하게 보관할 방법이 없다.

### 헬스케어

헬스케어 제공자는 블록체인을 활용하여 환자의 의료 기록을 안전하게 저장할 수 있다. 의료 기록이 생성되고 서명되면 블록체인에 기록이 가능하여 환자들에게 기록 변경이 불가능하다는 증명과 자신감을 제공한다. 이러한 개인 의료 기록은 개인 키와 함께 암호화되어 저장되어 특정 개인만이 접근할 수 있도록하여 프라이버시를 보장할 수 있다.

### 재산 기록(Property Records)

네가 만약 지역 사무국에서 시간 쓴 경험이 있다면, 재산권 기록이 얼마나 부담스럽고 비효율적인지 잘 알 것이다. 오늘날, 물리적 증서는 수동으로 국가 중앙 데이터베이스에 입력되는 지역 사무국의 공무원에게 배달되어야 한다. 재산 분쟁의 경우, 재산에 대한 청구권은 공적 지표(public index)와 맞아야 한다.

이 과정은 비용과 시간이 많이 소비되며, 사람이 실수하기도 쉽고 부정확할 때마다 부동산 소유권을 추적해야만하는 비효율이 발생한다. 블록체인은 문서를 스캔하고 지역 사무국의 물리적 기록을 추적해야하는 필요성을 제거할 수 있는 가능성을 가지고 있다. 소유권이 블록체인에 저장되고 확인된다면, 소유자는 그들의 증서가 정확하고 영구적으로 저장된다고 신뢰할 수 있다.

전쟁으로 피폐해져 정부나 금융 인프라가 제 기능을 못하거나 사무국이 없는 곳에서 소유권을 증명하기란 불가능에 가깝다. 그런 지역의 사람들이 블록체인을 활용할 수 있다면, 투명하고 정확한 재산 소유의 타임라인을 확립할 수 있다.

### 스마트 컨트랙트

스마트 컨트랙트는 블록체인이 계약 합의를 가능하게 하는 컴퓨터 코드이다. 스마트 컨트랙트는 사용자들이 동의하는 일련의 조건하에 운영된다. 조건들이 충족되면, 자동으로 계약 조건이 이행된다.

예를 들어, 세입자가 되고 싶은 사람이 스마트 컨트랙트를 활용하여 아파트를 빌릴 수 있다. 임대인은 세입자가 임대 보증금을 내는 즉시 세입자에게 아파트 집 비번을 알려주는 것을 동의한다. 스마트 컨트랙트는 보증금 지불 시 자동으로 집 비번을 세입자에게 전달할 것이다. 또한 보증금이 지불되지 않거나 다른 조건들을 만나게 된다면 비번이 바뀌도록 프로그래밍 돼있을 것이다.

### 공급망(Supply Chains)

IBM 식품 신뢰의 예시처럼, 공급자들은 그들이 구매한 재료의 출처에 대해 블록체인을 활용할 수 있다. 이를 통해 기업은 자사 제품 뿐 아니라 “유기능”, “로컬”, “공정 거래”와 같은 일반적인 라벨의 진위 여부를 확인할 수도 있다.

포브스의 보도에 따르면, 식품 산업은 농장에서 사용자로 이동하는 내내 식품의 경로와 안전성을 추적하기 위해 블록체인을 활용하는 사례가 늘어나고 있다고 한다.

### 투표

위에서 언급했듯, 블록체인은 현대 투표 시스템을 가능하게 한다. 블록체인을 활용한 투표는 2018년 11월 웨스트 버지니아주 중간 선거에서 검증된 바와 같이 블록체인을 이용한 투표는 부정선거를 없애고 투표율을 높일 수 있는 가능성을 가지고 있다.

이러한 방식의 블록체인 활용은 투표를 함부로 변경하는 것을 거의 불가능하게 만들 것이다. 블록체인 프로토콜은 또한 선거 프로세스에서 투명성을 유지하고 선거에 필요한 인력을 줄이고 공무원들에게 즉각적인 결과를 제공할 것이다. 이렇게 되면 재검표의 필요성이 없어지고 부정선거가 선거를 위협한다는 우려를 종식시킨다.

## 블록체인의 장단점

블록체인은 모든 복잡성에도 불구하고 분산된 형태의 기록 보관으로써 잠재력은 한계가 없다. 블록체인 기술은 사용자 개인정보 보호 강화와 보안 강화에서 처리 비용 절감과 오류 감소에 이르기까지 위에서 설명한 것 이상의 어플리케이션을 볼 수 있지만, 단점도 있다.

| 장점                                    | 단점 |
| --------------------------------------- | ---- |
| * 검증에 사람의 개입을 없애 정확도 향상 |      |

- 서드 파티 검증을 없애 비용 감소
- 탈중앙화를 통해 가로채기가 어려워짐
- 트랜잭션은 보안되고 프라이빗하고 효율적임
- 투명한 기술
- 정부가 불안정하거나 후진국의 시민들을 위해 은행 업무에 대한 대안과 개인 정보 확보의 방법을 제공 | * 일부 블록체인의 상당한 기술 비용
- 낮은 초당 트랜잭션
- 위법 행위에 사용된 전례가 있음 (다크 웹과 같은)
- 규제가 국가마다 다르고 불확실함
- 데이타 저장소가 제한됨 |

## 블록체인의 이점

### 체인의 정확성

블록체인 네트워크의 트랜잭션은 수천개의 컴퓨터와 장치에 의해 승인된다. 이는 검증 과정에서 거의 모든 사람을 제거하여 휴먼 에러를 줄이고 정확한 정보 기록을 가능하게 한다. 심지어 네트워크상 컴퓨터가 실수를 저질러도, 그 실수는 블록체인 한 본사본에만 이루어질 것이고 나머지 네트워크에서는 인정되지 않을 것이다.

### 비용 절감

보통 소비자들은 은행을 거래 확인이나 문자 서명 공증을 위해 소비한다. 블록체인은 이런 제 3자의 필요성과 비용을 없앤다. 예를 들어, 비즈니스 오너는 은행과 결제사는 그들의 신용 카드 거래를 위해 비용을 지불한다. 반면 비트코인은 중앙 관리자가 없고 제한된 거래 수수료를 가진다.

### 탈중앙화

블록체인은 정보를 중앙 저장소에 저장하지 않는다. 대신, 블록체인은 컴퓨터 네트워크 전반에 복사하여 저장한다. 블록체인에 새로운 블록이 저장될 때마다, 네트워크의 모든 컴퓨터는 변경을 반영하고 블록체인을 업데이트한다.

네트워크 전반에 정보를 뿌려놓음으로써, 중앙 데이터베이스에 저장하는 것보다 블록체인에서는 정보 갈취가 어려워진다.

### 효율적인 거래

중앙 관리를 거치는 거래는 몇일이 걸린다. 예를 들어, 만약 네가 금요일 저녁에 예금을 시도한다면 그 반영은 월요일이 되서야 볼 수 있을 것이다. 금융 기관은 영업일에만 운영한다.

몇몇 블록체인에서 거래는 몇 분 안에 안전한 거래를 완료한다. 이는 특히 외화간 거래에 유용하다. 타임존이 다르고 각각 국가에서 지불 확인 절차가 필요하기 때문이다.

### 개인 거래

많은 블록체인 네트워크는 인터넷에 연결된 누구나 네트워크의 거래 기록을 확인할 수 있는 공개 데이터베이스 하에 운영된다. 사용자가 거래 상세를 볼 수 있음에도, 그들은 해당 트랜잭션을 수행하는 사용자에 대한 식별 정보에는 접근할 수 없다. 이는 비트코인과 같은 블록체인 네트워크가 완전히 익명성이라는 흔한 오해이다. 정보가 유출되면 사용자와 연관될 수 있는 보이는(식별 가능한?)주소가 있기에 실제로는 가명이다.

### 보안 거래

트랜잭션이 기록될 때, 거래의 진위는 블록체인 네트워크에 의해 확인된다. 트랜잭션이 검증된 뒤, 블록체인 블록에 추가된다. 블록체인의 각 블록은 유니크한 해시와 이전 블록의 유니크 해시를 포함한다. 그러므로 블록들은 네트워크가 확인할 때 바뀔 수 없다.

### 투명성

대부분의 블록체인은 오픈소스다. 이는 모든 사람들이 그것의 코드를 볼 수 있음을 의미한다. 이를 통해 감사는 보안을 위해 비트코인과 같은 암호화폐를 검토할 수 있다. 그러나, 비트코인의 코드를 누가 통제하는지, 어떻게 편집하는지에 대한 실질적인 권한이 없다는 것을 의미하기도 한다. 이러한 이유로, 누구나 시스템의 변경이나 업데이트를 제안할 수 있다. 네트워크 사용자 과반이 업그레이드와 함께 코드의 새로운 버전이 건전하고 가치 있다 동의하면 비트코인을 업데이트 할 수 있다.

### Banking the Unbanked

아마 블록체인과 암호화폐의 가장 심오한 측면은 민족, 성별, 지역, 문화적 배경에 관계없이 누구나 사용할 수 있는 능력일 것이다. The World Bank에 따르면, 대략 13억명의 성인들이 은행 계좌를 갖고 있지 않거나 그들의 돈이나 재산을 보관할 어떤 수단도 가지고 있지 않는다고 한다. 게다가, 이들 중 대부분은 경제가 초기 단계이고 현금 의존적인 개발도상국에 거주하고 있다.

이런 사람들은 주로 물리적 현금으로 결제한다. 그들은 물리적 현금을 강도나 폭력에 노출될 수도 있는 집과 같은 숨겨놓을 만한 장소에 보관해야 한다. 도둑 맞는 것이 불가능해지려면, 암호화폐는 도둑들이 훨씬 어렵게 만들 수 있다.

또한 미래의 블록체인은 재화 보관의 계좌 뿐 아니라 의료 기록, 소유권, 다양한 법적 계약의 저장에도 해결책을 찾고 있다.

## 블록체인의 단점

### 기술 비용

블록체인은 사용자의 거래 수수료를 절약 할 수 있지만, 그렇다고 공짜는 아니다. 예를 들어, 비트코인 네트워크의 거래 검증을 위한 작업 증명 시스템은 상당한 양의 계산 능력을 소비한다. 실세계에서, 비트코인 네트워크에서 소비되는 수백만 장치의 에너지는 파키스탄 1년 소비 에너지보다 많다.

이러한 문제의 몇몇 해결책은 슬슬 제시되고 있다. 예를 들어, 비트코인 채굴장이 태양력 발전, 과도한 천연가스 시추장, 풍력 발전 등을 사용하려는 노력 등이 있다.

### 속도와 데이터 비효율성

비트코인은 블록체인의 비효율 가능성을 공부할 수 있는 최고의 사례이다. 비트코인의 PoW 시스템은 새로운 블록을 블록체인에 추가하는데에 약 10분이 소요된다. 이런 속도라면 블록체인 네트워크는 초당 약 3개의 트랜잭션(transactions per second:TPS)만 관리할 수 있는것으로 추정된다. 이더리움과 같은 다른 암호화폐는 비트코인보다 나은 성능을 가지지만, 여전히 블록체인은 제한적인 속도를 가지고 있다. 현존 브랜드인 비자는 65,000 TPS를 처리할 수 있다.

개발계에서 몇년간 이 문제를 해결하려 노력했다. 현재 블록체인은 30,000TPS이상을 처리할 수 있다. 2022년 9월 15일, 이더리움 메인넷과 비콘 체인간의 머지는 더 많은 장치(핸드폰, 태블릿 및 노트북)가 이더리움을 실행할 수 있도록 데이터베이스 분할을 포함한 일련의 업그레이드를 출시하였고 최대 100,000TPS를 가능케 할 수 있을것으로 예상된다. 이는 네트워크 참여를 증가시키고, 혼잡을 줄이며, 거래 속도를 증가시킬 것으로 예상된다.

다른 이슈로, 각 블록이 너무 많은 데이터를 가지고 있다는 점이 있다. 블록 사이즈 토론은 블록체인이 확장성을 위해 나아가야할 가장 큰 과제 중 하나이다.

### 위법 행위

블록체인의 사용자 해킹 보호와 개인정보 보호에의 자신감에도, 블록체인 네트워크에는 불법 거래또한 가능케한다. 불법거래에 블록체인이 사용된 가장 유명한 사례는 아마 실크로드일 것이다.

다크웹은 사용자가 유명 브라우저를 사용하여 추적받는 것을 방지하고 비트코인이나 다른 암호화폐를 활용해 불법적인 물건을 사고 파는 곳이다. 이는 금융 서비스 제공자가 계좌 개설 시 고객에 대한 정보를 얻도록 요구하는 미국의 규정과 상반된다. 금융 서비스 제공자는 각 고객의 신원을 확인하고 테러 단체에 연루돼있지는 않은지 확인한다.

> **중요** 2022년 불법 행위에 암호화폐가 사용된 사례는 0.24%에 불과하다.

블록체인은 장점과 단점 모두 볼 수 있다. 블록체인은 누구나 금융 계좌에 접근할 수 있게하지만, 범죄에 쉽게 접근할 수 있게도 한다. 많은 이들이 banking the unbanbked world와 같은 암호화폐의 좋은 사용이 암호화폐의 나쁜 사용보다 효용이 더 크다고 성토한다.

### 규제

암호화폐 분야의 많은 이들이 암호화폐에 대한 정부 규제에 대한 우려를 표한다. 분산 네트워크가 커지면서 비트코인과 같은 네트워크를 끝내는 것이 점점 어려워지고 있고 거의 불가능해지지만, 정부는 이론적으로 암호화폐를 소유하거나 네트워크에 참여하는 것을 불법으로 간주할 수도 있다.

페이팔과 같은 대기업들이 고객들이 전자상거래 플랫폼에서 암호화폐를 사용할 수 있도록 허용하기 시작하면서, 이러한 우려는 점차 작아지고 있다.

## 마치며

기술에 대한 많은 실용적 어플리케이션이 이미 구현되고 탐구되고 있는 가운데, 블록체인은 마침내 비트코인과 암호화폐로 적잖은 부분에서 이름을 알리고 있다. 블록체인 투자자들이 말하는건, 블록체인은 더 적은 중간자들로 비즈니스와 정부 운영을 더 정확하고, 효율적이고 안전하고 저렴하게 만드는 것이다.

블록체인이 세 번째 10년으로 접어들며, 레거시 기업들이 기술을 따라잡을 것인지는 더 이상 고려할 필요가 없다. 언제가 될 지의 문제인 것이다. 오늘날 우리는 NFT의 확산과 자산의 토큰화를 볼 수 있다. 결과적으로 향후 수십 년은 블록체인의 중요한 성장 기간이 될 것이다.