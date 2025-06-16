# GAME

Animal Kingdom

게임 장르 : 로그라이크, 뱀파이어서바이벌, 멀티 게임(크로스 플랫폼은 추후 진행 예정)

====로그인

-게스트 로그인

Firebase FireStore 사용

(AWS를 구현하지 않은 상태이기때문에, Firebase Firestore의 테스트 모드로 임시 설정)

저장 :유저의 로컬 ID를 Key로 설정, USERDATA를 Serialized 후 Encrypt 저장

호출 :로컬 ID를 통해 유저의 정보를 Firebase에서 호출, Decrypt 후 <T>를 UserData로 Deserialied 변경

-구글 로그인

실행 방법

1.Firebasee 설정

2.플랫폼 Android로 Switch

3.fingerPrints 생성(SHA-1)

4.google-services.json 프로젝트에 추가

5.Firebase Auth 프로젝트에 Custom Import

6.Firebase Auth 추가로 생성된 dll에 플랫폼 설정

7.Resolve진행

====에셋 다운로드

-CDM

1.인게임에서 필요한 다운을 해야되는 리소스, 다운을 받을 필요없는 에셋으로 분류

2.Addressable 시스템을 이용하여, Git URL에서 에셋 다운 받게 설정 및 실행

(아직 완벽하게 분류를 해놓진 않은 상태)
