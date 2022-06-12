# Local Servers
로컬에서 사용중인 서버들의 도커 템플릿을 모아놓은 프로젝트 입니다. compose 파일 전에 도커 네트워크를 먼저 생성해야 합니다.
```
docker network create --driver bridge local
```
이후에 개별 서비스 폴더에서 컨테이너를 생성하면 됩니다.
```
docker compose up -d
```
