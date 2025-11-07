# Sealed Secret 사용 방법
1. secret yaml파일 준비
2. `cat secret.yaml | kubeseal -oyaml > sealed-secret.yaml`
3. `SealedSecret`리소스를 생성하면 내용을 토대로 `Secret`이 생성됨
4. 먼저 `SealedSecret` 배포 후 ArgoCD로 관리 시 `sealedsecrets.bitnami.com/managed: "true"`라는 `annoataions`를 넣어줘야 오류가 해결되는 경우가 있음.

# Helm 차트 값
- `keyRenewPeriod` 값을 `0`으로 주어 키 순환이 되지 않는 상태.
    - 키 순환 활성화 시 주기적으로 새 secret을 생성해줘야 하기 때문
- `fullnameOverride` 값을 `sealed-secrets-controller`로 주어 `kubeseal` 명령어 사용 시 기본값으로 컨트롤러를 찾아갈 수 있도록 설정