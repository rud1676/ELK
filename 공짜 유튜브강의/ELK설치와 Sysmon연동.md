## ELK + Sysmon

엘라스틱과 연동하면 시각화된 로그들을 손쉽게 볼수 있고 클릭한번으로 필터링이 가능함! 또한 옵션으로 실시간으로 전송이 가능!

## ELK와 Sysmon관계

1. 윈도우에서 데이터 수집(sysmon)
2. 데이터 전송(우분투 서버로 전송) - WinlogBeat
3. DB저장 - LogStash
4. 분석 Kiabana

## 우분투에서 설치된 Docker로 ELK설치

