# opendistro yml 정리

## secure

### 자격증명 흐름

1. 자격증명 방식엔 3가지 방법이 있음 (로그인방식, JSON token, TLS방식)

opendistrosecure 설정 바꾸는 cl

```
./securityadmin.sh -cd ../securityconfig/ -icl -nhnv  -cacert /etc/elasticsearch/certs/root-ca.pem -cert /etc/elasticsearch/certs/admin.pem -key /etc/elasticsearch/certs/admin.key
```
