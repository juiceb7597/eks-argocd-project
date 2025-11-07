# GitOps for ArgoCD 
- Multi Cluster 환경 ArgoCD App of Apps 구조 프로젝트

## 아키텍처

![Alt text](./img/architecture.png)

## App of Apps 구조

![Alt text](./img/application-structure.png)

## 폴더 구조

<table border="1" cellpadding="6" cellspacing="0" style="border-collapse: collapse; font-family: Arial, sans-serif;">
  <thead>
    <tr style="background-color:#f0f0f0;">
      <th>깊이</th>
      <th>폴더</th>
      <th>설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td><span style="color:#FFFFFF; background-color:#FF6B6B; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├argocd</span></td>
      <td>ArgoCD application 리소스 집합</td>
    </tr>
    <tr>
      <td>1</td>
      <td><span style="color:#FFFFFF; background-color:#4ECDC4; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├──bootstrap</span></td>
      <td>Root Application (전체 서비스 모듈 및 인프라)</td>
    </tr>
    <tr>
      <td>1</td>
      <td><span style="color:#FFFFFF; background-color:#4ECDC4; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├──infrastructure</span></td>
      <td>인프라 Application 리소스 집합</td>
    </tr>
    <tr>
      <td>2</td>
      <td><span style="color:#FFFFFF; background-color:#45B7D1; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├────인프라 구성요소 (예: albc)</span></td>
      <td>인프라 구성요소 Application 리소스</td>
    </tr>
    <tr>
      <td>3</td>
      <td><span style="color:#FFFFFF; background-color:#96CEB4; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├──────web/was-cluster</span></td>
      <td>클러스터별 설정</td>
    </tr>
    <tr>
      <td>0</td>
      <td><span style="color:#FFFFFF; background-color:#FF6B6B; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├apps</span></td>
      <td>서비스 모듈 리소스 집합</td>
    </tr>
    <tr>
      <td>1</td>
      <td><span style="color:#FFFFFF; background-color:#4ECDC4; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├──서비스 모듈명</span></td>
      <td>특정 서비스 모듈 리소스 집합</td>
    </tr>
    <tr>
      <td>2</td>
      <td><span style="color:#FFFFFF; background-color:#45B7D1; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├────application</span></td>
      <td>서비스 모듈 application 리소스</td>
    </tr>
    <tr>
      <td>3</td>
      <td><span style="color:#FFFFFF; background-color:#96CEB4; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├──────base</span></td>
      <td>공통 리소스</td>
    </tr>
    <tr>
      <td>3</td>
      <td><span style="color:#FFFFFF; background-color:#96CEB4; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├──────overlays</span></td>
      <td>클러스터별 오버레이</td>
    </tr>
    <tr>
      <td>4</td>
      <td><span style="color:#333333; background-color:#FFEAA7; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├────────web/was-cluster</span></td>
      <td>클러스터별 설정</td>
    </tr>
    <tr>
      <td>2</td>
      <td><span style="color:#FFFFFF; background-color:#45B7D1; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├────resources</span></td>
      <td>서비스 모듈 리소스 집합</td>
    </tr>
    <tr>
      <td>3</td>
      <td><span style="color:#FFFFFF; background-color:#96CEB4; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├──────base</span></td>
      <td>공통 리소스</td>
    </tr>
    <tr>
      <td>3</td>
      <td><span style="color:#FFFFFF; background-color:#96CEB4; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├──────overlays</span></td>
      <td>클러스터별 오버레이</td>
    </tr>
    <tr>
      <td>4</td>
      <td><span style="color:#333333; background-color:#FFEAA7; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├────────web/was-cluster</span></td>
      <td>클러스터별 설정</td>
    </tr>
    <tr>
      <td>0</td>
      <td><span style="color:#FFFFFF; background-color:#FF6B6B; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├infrastructure</span></td>
      <td>인프라 구성요소 리소스 집합</td>
    </tr>
    <tr>
      <td>1</td>
      <td><span style="color:#FFFFFF; background-color:#4ECDC4; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├──인프라 구성요소 (예: albc)</span></td>
      <td>인프라 리소스 집합</td>
    </tr>
    <tr>
      <td>2</td>
      <td><span style="color:#FFFFFF; background-color:#45B7D1; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├────application</span></td>
      <td>추가 리소스용 Application 리소스</td>
    </tr>
    <tr>
      <td>3</td>
      <td><span style="color:#FFFFFF; background-color:#96CEB4; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├──────base</span></td>
      <td>공통 리소스</td>
    </tr>
    <tr>
      <td>3</td>
      <td><span style="color:#FFFFFF; background-color:#96CEB4; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├──────overlays</span></td>
      <td>클러스터별 오버레이
    </tr>
    <tr>
      <td>4</td>
      <td><span style="color:#333333; background-color:#FFEAA7; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├────────web/was-cluster</span></td>
      <td>클러스터별 설정</td>
    </tr>
    <tr>
      <td>2</td>
      <td><span style="color:#FFFFFF; background-color:#45B7D1; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├────helm</span></td>
      <td>Helm 차트 Application 리소스</td>
    </tr>
    <tr>
      <td>3</td>
      <td><span style="color:#FFFFFF; background-color:#96CEB4; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├──────base</span></td>
      <td>공통 리소스</td>
    </tr>
    <tr>
      <td>3</td>
      <td><span style="color:#FFFFFF; background-color:#96CEB4; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├──────overlays</span></td>
      <td>클러스터별 오버레이
    </tr>
    <tr>
      <td>4</td>
      <td><span style="color:#333333; background-color:#FFEAA7; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├────────web/was-cluster</span></td>
      <td>클러스터별 설정</td>
    </tr>
    <tr>
      <td>2</td>
      <td><span style="color:#FFFFFF; background-color:#45B7D1; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├────resources</span></td>
      <td>추가 리소스 집합</td>
    </tr>
    <tr>
      <td>3</td>
      <td><span style="color:#FFFFFF; background-color:#96CEB4; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├──────base</span></td>
      <td>공통 리소스</td>
    </tr>
    <tr>
      <td>3</td>
      <td><span style="color:#FFFFFF; background-color:#96CEB4; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├──────overlays</span></td>
      <td>클러스터별 오버레이
    </tr>
    <tr>
      <td>4</td>
      <td><span style="color:#333333; background-color:#FFEAA7; font-weight:bold; padding: 2px 4px; border-radius: 3px;">├────────web/was-cluster</span></td>
      <td>클러스터별 설정</td>
    </tr>
  </tbody>
</table>