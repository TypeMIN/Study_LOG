## Confidentiality
> 기밀성(Confidentiality) : 권한이 없는 사용자가 정보를 사용할 수 없도록 하는 것

- 데이터를 보호
- 데이터를 열람할 수 있는 사용자에게 권한 부여
- 권한이 없는 사람이 데이터로부터 정보를 얻는 것 불허
### How to achieve Confidentiality
#### Encryption
> 암호화 (Encryption) : 허용된 사람들을 제외하고는 누구든지 읽어볼 수 없도록 알고리즘을 이용하여 정보를 전달하는 과정

- Encryption Key를 이용하여 정보를 변환
- Decryption Key를 소유하고 있는 사용자만이 정보를 읽을 수 있음
##### Schemes
- 대칭 키 암호화 (Symmetric-key encryption)
- 비대칭 키 암호화 (Asymmetric-key encryption)
#### Access Control
> 접근 제어 (Access Control) : 누군가가 무언가를 사용하는 것을 허가하거나 거부하는 기능

- 기밀 정보에 대한 접근을 제한하는 규칙과 정책
- 사용자마다 수행할 수 있는 작업에 대한 권한 결정
- 권한은 신원 또는 역할에 따라 결정
#### [[Authentication]]
> 인증 (Authentication) : 통신 상에서 보내는 사람의 디지털 정체성을 확인하는 시도의 과정