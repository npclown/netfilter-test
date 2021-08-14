## report netfilter test
###과제
netfilter를 이용하여 유해 사이트를 차단하라.

###실행
```
syntax : netfilter-test <host>
sample : netfilter-test test.gilgil.net
```
###상세
- iptables 명령어를 이용하셔 송수신되는 모든 패킷을 netfilter queue로 jump시킨다.
- netfilter 예제에서 nfq_get_payload 이후 패킷의 시작 위치와 패킷의 길이를 알아내고 나서 IP, TCP, HTTP 형식으로 parsing을 한다.
- 평문 통신하는 사이트를 대상으로 한다(HTTPS 통신하는 사이트는 제외). HTTP Request에서 Host 필드를 추출한 다음 Host 값이 인자와 같은 경우 유해 사이트라 판단한다.
- 유햬 사이트라고 판단되는 경우 nfq_set_verdict 함수의 3번째 인자를 NF_ACCEPT에서 NF_DROP으로 변경하여 함수를 호출하여 트래픽이 차단되는지 확인한다.
