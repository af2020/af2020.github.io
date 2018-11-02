
# docker 명령어 정리

지속적으로 업데이트하면서 자주 사용하는 명령어를 정리

## docker 구성

docker를 사용하면 리눅스 시스템의 복잡한 설정을 위해서 필요한 작업을 깔끔하게 정리할 수 있는데, 잘 만들어진 docker image를 load하여 사용할 수 있기 때문이다. 여러 가지 옵션을 통해서 docker를 통제할 수 있는데, 주요 구성 사항을 정리하면 다음과 같다.

* jupyter kernel: R, Python, Scala
* library, package 업데이트 사항은 image로 지속적으로 업데이트
* 분석 내용이 담겨 있는 file 저장을 위한 외부 볼륨 지정

### docker load 


```python
sudo docker run -d --rm -p *****:8888 -e JUPYTER_LAB_ENABLE=yes -v "$PWD":[work directory] [docker image]:[tag]
```
