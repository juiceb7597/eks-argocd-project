# ArgoCD Image Updater Pod Identity 적용 방법
1. `AmazonEC2ContainerRegistryReadOnly` 권한을 가진 역할(Pod Identity 신뢰관계)을 만든다.
2. ArgoCD Image Updater를 배포한다
3. 생성된 Service Account에 해당 역할로 Pod Identity를 연결한다.

# ArgoCD 연결 방법 
1. `ARGOCD_TOKEN` 환경변수를 등록한다. (https://argocd-image-updater.readthedocs.io/en/stable/install/installation/#configure-api-access-token-secret)
2. ArgoCD에서 Image Updater가 사용할 토큰을 생성한다. (여기서는 App Project의 Token 사용)
    - `argocd proj role create-token <PROJECT-NAME> <ROLE-NAME>`
3. ArgoCD에서 `argocd.token`을 키로 Secret을 생성한다.

# Git 연결 방법
1. ArgoCD에서 사용하는 Git credential을 재사용한다. (https://argocd-image-updater.readthedocs.io/en/stable/basics/update-methods/#specifying-git-credentials)
2. 적용할 `Application` 리소스에 `annotations` 를 추가한다. 

```yaml
...
    argocd-image-updater.argoproj.io/write-back-method: git:repocreds #Or git:secret:argocd/gitea-creds
    argocd-image-updater.argoproj.io/image-list: test=<Account-Number>.dkr.ecr.<Region>.amazonaws.com/test/test
    argocd-image-updater.argoproj.io/test.update-strategy: alphabetical
...
```