# OCI

## CONCEPT

### Fault Domains

Availability Domain 내에 하드웨어와 인프라스트럭쳐의 그룹

각 Availability Domain은 3개의 Fault Domain을 가진다. \
Fault Domain은 Compute 인스턴스를 단일 Availability Domain 내에 하나의 물리적 하드웨어에 분배하지 않도록 한다.

### Compartment

Compartment는 자원들을 쉽게 관리할 수 있도록 하는 개념으로 폴더 구조\
Tenancy가 생성되면 최초로 Root Compartment 하나가 만들어진다. 관리자가 Root Compartment 하위로 새로운 Compartment를 추가할 수 있다.\
모든 OCI 자원들은 특정 Compartment에 속하게 되며 Compartment 단위로 사용자들의 접근 정책을 관리한다.

