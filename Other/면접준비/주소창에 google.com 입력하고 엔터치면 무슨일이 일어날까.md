# 주소창에 google.com 입력하고 엔터치면 무슨일이 일어날까?

## 1. google.com 을 브라우저 주소창에 입력한다.

## 2. Browser는 캐싱된 DNS 기록을 통해 google.com에 대응되는 IP 주소가 있는지 확인한다.

### 브라우저 캐시?

#### 브라우저 캐시란?

* 브라우저에서 `로컬 웹 페이지 리소스`를 저장하는 데 사용되는 `매커니즘`
* 캐시를 통해 성능 향상 및 대역폭 소비가 최소화되어 개선된 환경 가능

#### 방식

* 브라우저가 웹 서버의 일부 컨텐츠 요청
* 컨텐츠가 브라우저 캐시에 없으면 웹 서버에서 직접 검색
* 컨텐츠가 이전에 캐시 됐다면 브라우저는 서버를 우회하여 캐시에게 직접 컨텐츠 로드
* 캐시된 컨텐츠 만료 여부에 따라 컨텐츠가 `Stale`인 것으로 간주 (stale: 탁한)
  * 반면, `Fresh`는 컨텐츠가 
    * 만료 날짜를 안지났고
    * 서버가 아닌 브라우저 캐시에서 직접 제공 될 수 있음 의미
* 유효성 검사
* 
  * 서버가 보유하고 있는 최신 버전과 비교하여 검사해야하는 컨텐츠
  * 즉, 내용이 `stale`인지 여부 판단
  * 유효기간 만료 전 캐시에서 내용 제거하면 유효성 확인되지 않음
  * 내용 변경된 경우 서버에서 강제 될 수 있으며 문제 발생하지 않도록 브라우저에 최신 버전 있어야 함
* 브라우저 캐싱은 특정 HTTP Header를 사용하여 웹 개발자와 관리자가 활용 가능



### DNS??

* **Domain Name System**
* IP 네트워크에서 사용하는 시스템
* 왜 있어??
  * 유저가 인터넷을 편하게 이용할 수 있게 함
  * 이거 없으면 유저는 ip 주소 직접 쳐서 사이트에 접속해야 함
* 영문/한글 주소를 IP 네트워크에서 찾아갈 수 있는 IP로 변환해 줌
* 이 DNS를 운영하는 서버를 네임서버`Name Server`라고 부름
  * 규모가 있는 사이트의 경우 네임서버를 자체 운영하는 경우도 있음



* 인터넷에 있는 모든 URL에는 고유의 IP address 가 있음

* 이 IP 주소를 통해 해당 웹사이트를 호스팅하고 서버 컴퓨터에 접근 가능

* ```bash
  nslookup www.google.com
  ```

* 위와 같은 명령어를 통해 해당 사이트의 IP 주소를 확인할 수 있음

  * `www.google.com`의 경우 사용자가 많아 서버 IP 주소가 여러개
  * 그 중에서 내가 접속 할 수 있는 IP 주소를 알려주는 것임

* 이와같이 DNS는 전화번호부와 비슷한 역할을 한다.

* 웹사이트 이름과 접근을 위한 IP주소를 저장하고 있는 것임!

  * 유저가 우베사이트 주소 쉽게 접속할 수 있게 `매핑`시켜주는 역할

* 웹사이트 이름 브라우저에 입력 시 DNS 기록을 4가지의 `Cache`에서 확인

  1. 브라우저 캐시
     * 브라우저는 일정 기간 동안 유저가 이전 접속한 DNS 기록들 저장하고 있음
     * `DNS query`가 이 곳에서 가장 먼저 실행됨
  2. OS 캐시
     * 브라우저 캐시에 웹사이트 이름 IP 주소가 없다?
     * 브라우저는 `systemcall`을 통해 OS가 저장하고 있는 DNS 기록들의 캐시에 접근
  3. router 캐시
     * 컴퓨터에 DNS 기록 못 찾았다?
     * 브라우저는 DNS 기록을 캐싱하고 있는 router와 통신하여 찾으려 함
  4. ISP 캐시
     * ISP
       * Internet Service Provider
       * 개인이나 기업체에 인터넷 접속 서비스, 웹사이트 구축 및 웹 호스팅 서비스를 제공하는 회사
       * ex) KT, SK, LG U+ 등
     * IPS는 DNS 서버를 구축하고 있음
     * 브라우저가 마지막으로 DNS 기록이 있길 바라며 접근

* 왤케 캐시 저장한 곳이 많아요??

  * 캐시는 네트워크 트래픽을 조절하고 데이터 전송 시간을 줄이기 위해 매우 중요하기 때문!



## 3. 요청한 URL이 캐시에 없으면, ISP의 DNS 서버가 `www.google.com`을 호스팅하고 있는 서버의 IP 주소를 찾기 위해 DNS query를 날린다.

* 앞서 말했듯이 `www.google.com`에 접속하고 싶으면 IP 주소를 반드시 알아야 함
* DNS query의 목적
  * 여러 다른 DNS 서버들을 검색해 해당 사이트의 IP 주소를 찾는 것
  * 이러한 검색을 `recursive search`
  * IP 주소를 찾을 때 까지 DNS 서버에서 다른 DNS 서버를 오가면서 반복적으로 검색하던지
  * 못 찾아서 에러 발생할 때 까지 검색 진행
* 이러한 recursive search 상황에서
  * ISP의 DNS 서버 : DNS recursor
  * 다른 DNS 서버 : name server
  * 이들은 웹사이트 도메인 이름의 구조에 기반해서 검색하기 때문







## 참고 링크

* 브라우저 캐시 : https://sarc.io/index.php/miscellaneous/1565-browser-cache
* Browser 에 URL 을 입력하고 enter 를 치면 무슨일이 일어날까? : https://blog.yevgnenll.me/posts/what-happen-browser-after-url-enter
* [번역] Browser에 www.google.com을 검색하면 어떤 일이 일어날까? : https://devjin-blog.com/what-happen-browser-search/
* What Happens When You Type google.com Or Any Other URL In Your Browser And Press Enter : https://www.linkedin.com/pulse/what-happens-when-you-type-googlecom-any-other-url-buitrago-vargas
* What happens when you type a URL in the browser and press enter? : https://medium.com/@maneesha.wijesinghe1/what-happens-when-you-type-an-url-in-the-browser-and-press-enter-bb0aa2449c1a
* DNS 
  * https://aws.amazon.com/ko/route53/what-is-dns/
  * https://www.cloudflare.com/ko-kr/learning/dns/what-is-dns/

