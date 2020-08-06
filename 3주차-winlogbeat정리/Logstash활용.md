# How to Use Logstash

[참고링크](https://medium.com/day34/elk-stack%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%A1%9C%EA%B7%B8-%EA%B4%80%EC%A0%9C-%EC%8B%9C%EC%8A%A4%ED%85%9C-%EB%A7%8C%EB%93%A4%EA%B8%B0-ca199502beab)

elastic cloud에 대하여 질문입니다!

현재 원하는 cloud사용은

1. winlogbeat를 통해 각 client의 로그를 수집
2. 수집된 log들을 logstash를 통해 필터링후 엘라스틱 cloud에 전송
3. cloud에서 시각화

인데 elastic cloud를 처음 사용했는데

로그스테쉬를 따로 설치하는 기능이 없더라구요

제가 실습을 했을 땐 클라우드 환경에서 한게아니라 VM환경에서 Ubuntu로 실습을 진행하여 elasticsearch, kibana ,logstash를 엘라스틱 서버쪽에 모두 설치하여 활용하였습니다.

그렇다면 elastic cloud에서는 logstash를 사용하려면 

아마존 ec2나 azure에서 가상컴퓨터를 만들어주고 그 컴퓨터에 logstash를 설치하고 각 client에서 수집되는 로그를 만들어준 logstash에 전송하고 또다시 logstash에서 elastic cloud로 전송하는 방식으로 만들어야되는지 궁금합니다.