## filter를 위한 KQL

[참고사이트](https://goateedev.tistory.com/109) - 정리할께 따로 없엇다 너무 간단..

## message부분 추출을 위한 GROK문법

mutate기법을 사용해봄.
[링크](https://bactoria.github.io/2020/04/12/%EB%A1%9C%EA%B7%B8%EC%8A%A4%ED%83%9C%EC%8B%9C-mutate-filter-plugin-%ED%8C%8C%ED%97%A4%EC%B9%98%EA%B8%B0/)로 시도함

정규식 기반으로 filtering 작성

```javascript
filter{
    if([event][code]==1){
        grok{
            match=>{"message"=>'.*?\n?RuleName: (?<RuleName>.+\n).*?UtcTime: (?<UtcTime>.+\n).*?ProcessGuid: (?<ProcessGuid>.+\n).*?ProcessId: (?<ProcessId>.+\n).*?Image: (?<Image>.+\n).*?FileVersion: (?<FileVersion>.+\n).*?Description: (?<Description>.+\n).*?Product: (?<Product>.+\n).*?Company: (?<Company>.+\n).*?OriginalFileName: (?<OriginalFileName>.+\n).*?CommandLine: (?<CommandLine>.+\n).*?CurrentDirectory: (?<CurrentDirectory>.+\n).*?User: (?<User>.+\n).*?LogonGuid: (?<LogonGuid>.+\n).*?LogonId: (?<LogonId>.+\n).*?TerminalSessionId: (?<TerminalSessionId>.+\n).*?IntegrityLevel: (?<IntegrityLevel>.+\n).*?Hashes: (?<Hashes>.+\n).*?ParentProcessGuid: (?<ParentProcessGuid>.+\n).*?ParentProcessId: (?<ParentProcessId>.+\n).*?ParentImage: (?<ParentImage>.+\n).*?ParentCommandLine: (?<ParentCommandLine>.+)'}
        }
        mutate {
         convert=>["RuleName","string"]
         convert => {
           "UtcTime" => "string"
           "ProcessGuid" => "string"
           "ProcessId" => "string"
           "Image" => "string"
           "FileVersion" => "string"
           "Description" => "string"
           "Product" => "string"
           "Company" => "string"
           "OriginalFileName" => "string"
           "CommandLine" => "string"
           "CurrentDirectory" => "string"
           "User" => "string"
           "LogonGuid" => "string"
           "TerminalSessionId" => "string"
           "IntegrityLevel" => "string"
           "ParentProcessGuid" => "string"
           "Hashes" => "string"
           "ParentProcessId" => "string"
           "ParentImage" => "string"
           "ParentCommandLine" => "string"
          }
          remove_field => ["message"]
        }
    }
}
```

와우 메세지 필터링 성공!.. => 그러나 mapping이 안되서 그걸 해결해야됨. - mutate convert로 작성하여 필터링중

-> 확인결과 message영역이 event_data. 어쩌구로 저장이됨. - javascript모듈설정을 푸니 제대로 이렇게 나와서 헛수고 ㅠ

[logstash활용방안](https://www.elastic.co/kr/blog/a-practical-introduction-to-logstash)

[regex정규식테스트사이트](https://regex101.com/)

logstash yml 디버깅 하는법

```
sudo bin/logstash --config.test_and_exit -f <path_to_config_file>
or
/usr/share/logstash/bin/logstash --config.test_and_exit -f ./logstash.conf
```

- 해결이 안되는점. parsing은 되나 mutation과 removed field가 작동이 안됨 - grok match는 잘되는데 왜안될까 그 뒤에 있는건.. => 이게 된다면 필터링을 많이 시도할수 있을거같은데 왜안되냐...

- 12월 19일 추가: indexparttern을 새롭게 정의했더니 targetFilename이 string으로 잘 나옴... 흠..

## Query DSL

```
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "winlog.event_data.Image": "*Explorer.EXE*"
          }
        }
      ]
    }
  }
}
```

C:\\Windows\*
