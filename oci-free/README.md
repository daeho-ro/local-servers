# OCI Free ARM Inatance Creator
본 이미지는 OCI에서 제공하는 무료 ARM 인스턴스 생성을 위한 자동 재시도 툴입니다. 이를 사용하기 위해서는 다음 작업을 진행해야 합니다.

- OCI 개인 키 생성 및 Credential 등록하기
- 인스턴스 생성을 위한 Stack 등록 후에 terraform 파일 다운로드하기
- 적절한 위치에 위 파일들을 넣고 컨테이너 구동하기

## 개인 키 생성

우측 상단의 내 아이콘을 클릭하여 User Settings에 들어갈 수 있습니다. 여기에서 API Keys 탭을 찾고 Add API Key를 눌러 Private Key를 다운로드 합니다. 저장된 파일을 `~/.ssh/oci.pem` 경로로 옮깁니다. 이후에 Configuration 파일 정보를 제공해주는데, 해당 내용을 복사하여 `~/.oci/config` 파일을 생성하고 그 내용을 붙어녛습니다. key_file 경로는 방금 다운로드 받아서 저장한 Private Key 파일 위치를 적으면 됩니다.

```
[DEFAULT]
user=ocid1.user.oc1..******
fingerprint=41:******
tenancy=ocid1.tenancy.oc1..******
region=ap-seoul-1
key_file=~/.ssh/oci.pem
```

## Terraform 파일 다운로드

Compute > Instances > Create Instance를 눌러 원하는 설정으로 인스턴스 생성을 준비합니다. 그리고 인스턴스를 생성하지 말고 Save as Stack을 눌러 스택을 생성합니다. 생성된 스택에서 우측의 Terraform Configuration 항목을 찾아 템플릿을 다운로드 할 수 있습니다. 압축을 해제하면 `main.tf` 파일이 있을텐데, 이 파일을 `data` 폴더에 넣습니다.

## 컨테이너 구동

OCI 설정 파일과 Private Key, Terraform 템플릿이 모두 준비되었습니다. 다음 명령을 통해서 컨테이너를 시작합니다.
```
docker compose up -d
```
로그를 확인하고 싶으면 docker의 내장 로그 기능을 사용합니다.
```
docker logs --follow oci-free
```
