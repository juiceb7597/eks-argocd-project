# ArgoCD Pod Identity 적용 방법
1. `eks:DescribeCluster` 권한을 가진 역할을 생성한다. 
  - 신뢰관계는 다음과 같다.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "pods.eks.amazonaws.com"
            },
            "Action": [
                "sts:AssumeRole",
                "sts:TagSession"
            ]
        },
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::<Account-Number>:role/<ArgoCD-Role-Name>"
            },
            "Action": [
                "sts:AssumeRole",
                "sts:TagSession"
            ]
        }
    ]
}
```
2. ArgoCD를 배포한다.
3. `argocd-server`, `argocd-applicationset-controller`, `argocd-application-controller` Service Account에 해당 역할로 Pod Identity를 연결한다.
4. 대상 EKS 클러스터의 IAM 엑세스 항목에 해당 역할을 추가한다.

# 대상 클러스터 연결 방법
1. `aws eks describe-cluster --name target-cluster-name --query "cluster.certificateAuthority.data" --output text` 명령으로 대상 클러스터의 base64 인코딩된 CA 데이터를 얻는다.
2. 대상 클러스터 인증 정보를 secret으로 등록한다.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: target-cluster-secret
  namespace: argocd
  labels:
    argocd.argoproj.io/secret-type: cluster
type: Opaque
stringData:
  name: "<Targe-Cluster-Name>"
  server: "https://75E1~~.eks.amazonaws.com"
  config: |
    {
      "awsAuthConfig": {
        "clusterName": "<Target-Cluster-Name>",
        "roleARN": "arn:aws:iam::<Account-Number>:role/<ArgoCD-Role-Name>"
      },
      "tlsClientConfig": {
        "insecure": false,
        "caData": "LS0tL~~~~"
      }
    }
```
3. ArgoCD UI > Settings > Clusters에서 대상 클러스터 연결 상태를 확인한다.

# Git 연결 방법
1. `argocd.argoproj.io/secret-type: repository` 레이블을 가진 secret을 생성한다. (https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/#repository-credentials)
2. 해당 시크릿에는 `url`, `username`, `password` 값이 포함된다.

```yaml
...
stringData:
  url: http://gitea-http.gitea.svc.cluster.local:3000/test/test.git
  username: argocd
  password: 3f28~~ # PAT
```
3. ArgoCD UI > Settings > Repositories에서 대상 Git 연결 상태를 확인한다.