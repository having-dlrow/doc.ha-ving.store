# - Git Branch 전략

## 대표적 전략

<table><thead><tr><th width="141"></th><th width="92">특징</th><th width="136">브랜치</th><th></th></tr></thead><tbody><tr><td>Git Flow</td><td>대규모</td><td><ul><li>feature</li><li>develop</li><li>release</li><li>hotfix</li><li>master</li></ul></td><td><img src="../../.gitbook/assets/image (21).png" alt="" data-size="original"></td></tr><tr><td>Github Flow</td><td>소규모</td><td><ul><li>main</li><li>develop</li><li>release</li><li>hotfix</li></ul></td><td><img src="../../.gitbook/assets/image (22).png" alt="" data-size="original"></td></tr></tbody></table>

### **Github Flow**

#### ① Branch 생성

* 새로운 기능이나 버그 수정 작업을 수행하기 위해 브랜치를 생성한다.
* 이 브랜치는 작업의 컨텍스트를 제공하고, 기능의 독립성을 보장한다.

#### ② Commit 작성

* 브랜치에서 변경 사항을 커밋으로 저장한다.
* 커밋은 작업의 단위이며, 코드 변경 내용을 기록한다.

#### ③ Pull Request

* 변경 사항을 본래 브랜치로 병합하기 위해 풀 리퀘스트를 생성한다.
* 이를 통해 코드 검토, 토론, 테스트 등을 수행할 수 있다.

#### ④ 리뷰 및 피드백

* 풀 리퀘스트를 생성한 후 다른 개발자들이 코드를 검토하고 피드백을 제공한다.
* 이를 통해 코드 품질을 높이고 버그를 발견하고 수정할 수 있다.

#### ⑤ 병합

* 풀 리퀘스트가 승인되면 변경 사항을 본래 브랜치로 병합한다.
* 이를 통해 작업한 내용이 제품의 다른 부분과 통합된다.

#### ⑥ 배포

* 병합된 변경 사항은 배포를 위한 브랜치로 이동하고, 자동 또는 수동으로 배포 프로세스를 시작한다.
* 배포 단계에서 테스트, 빌드, 배포 작업 등이 수행된다.



## 브랜치 전략 고려사항

* [ ] 제품으로 내보낼 것인가?
* [ ] 빌드 실패를 허용하는 가?
* [ ] 테스트 실패를 허용하는 가?
* [ ] 브랜치를 임시인가? 유지하지 않고 삭제하는가?
