## 자바 버전 변경하는 방법

리눅스에 자바가 여러개 설치되어있고 현재 사용중인 자바버전을 바꾸고 싶으면 다음 명령어를 사용한다
> `sudo update-alternatives --config java`


```bash
$ java -version                                                                                  
openjdk version "11.0.12" 2021-07-20
OpenJDK Runtime Environment (build 11.0.12+7-post-Raspbian-2deb10u1)
OpenJDK Server VM (build 11.0.12+7-post-Raspbian-2deb10u1, mixed mode)
$ sudo update-alternatives --config java                                                         
대체 항목 java에 대해 (/usr/bin/java 제공) 2개 선택이 있습니다.

  선택       경로                                          우선순위 상태
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-armhf/bin/java      1111      자동 모드
  1            /usr/lib/jvm/java-11-openjdk-armhf/bin/java      1111      수동 모드
  2            /usr/lib/jvm/java-8-openjdk-armhf/jre/bin/java   1081      수동 모드

Press <enter> to keep the current choice[*], or type selection number: 2
update-alternatives: using /usr/lib/jvm/java-8-openjdk-armhf/jre/bin/java to provide /usr/bin/java (java) in manual mode
$ java -version                                                                                  
openjdk version "1.8.0_312"
OpenJDK Runtime Environment (build 1.8.0_312-8u312-b07-1~deb9u1-b07)
OpenJDK Client VM (build 25.312-b07, mixed mode)
```
