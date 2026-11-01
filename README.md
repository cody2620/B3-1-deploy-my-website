# 내가 만든 웹사이트를 인터넷에 올려 누구나 쓰게 하기

## 메모
✅

## 아키텍처 다이어그램

## 웹 서비스 외부 접속 증빙

## 트러블 슈팅 보고서

## 리소스 체크리스트

***

<details>
  <summary> 기능 요구사항 </summary>

  1. 네트워크 구성

    * VPC 1개를 생성한다.
    * Public Subnet 1개를 생성한다.
    * Internet Gateway를 VPC에 연결한다.
    * Public Subnet의 Route Table에 `0.0.0.0/0 → Internet Gateway` 경로가 존재해야 한다.
    * Public Subnet에 배치된 인스턴스는 인터넷으로 아웃바운드 통신이 가능해야 한다. (예: `curl https://example.com` 성공)

2. 컴퓨트 및 웹 서버 배포

    * Public Subnet에 EC2 인스턴스 1대를 생성한다.
    * SSH로 인스턴스에 접속할 수 있어야 한다.
    * 웹 서버(Nginx 등)를 설치하고 실행 상태여야 한다.
    * 인스턴스에서 `curl http://localhost` 요청이 200 응답을 반환해야 한다.

3. 접근 제어(보안 그룹)

    * Security Group 인바운드는 원칙적으로 필요한 포트만 허용한다.
    * HTTP(80)는 `0.0.0.0/0`에서 접근 가능해야 한다.
    * SSH(22)는 학습자 개인 IP(또는 지정된 IP 대역)에서만 접근 가능해야 한다.
    * `0.0.0.0/0`에 대해 전체 포트(0-65535) 허용 규칙은 생성하지 않는다.

4. 권한(IAM) 최소권한

    * 실습에 사용하는 IAM 사용자(또는 Role) 1개를 사용한다.
    * 해당 IAM 권한은 EC2/VPC/Security Group 구성에 필요한 범위로 제한한다.
        * 예: 생성·조회·태그·연결 등 실습에 필요한 작업 중심
        * 예: 실습과 무관한 서비스(S3/RDS 등) 권한은 부여하지 않음
    * 관리자 권한(AdministratorAccess)은 부여하지 않는다.

5. 외부 접속 검증(택 1)

    * 아래 방식 중 1개를 선택해 "외부에서 접속 가능"을 증명해야 한다.
        * (A) 브라우저에서 `http://<퍼블릭IP>`로 접속했을 때 페이지가 정상 표시된다.
        * (B) `GET http://<퍼블릭IP>/health` 호출이 200을 반환하며 고정된 응답(예: "OK")을 확인할 수 있다.
    * 선택한 방식(A/B)은 `README.md`에 명시한다.

6. 운영 안정성(과금 방지)

    * 실습 종료 후, 생성한 리소스를 정리하고 체크리스트에 "종료/삭제 완료" 근거를 남긴다.
    * 최소한 다음 항목은 정리 완료를 확인해야 한다: EC2, EBS(볼륨), Elastic IP, Internet Gateway, VPC


  1. 네트워크 구성
  
  
  2. 컴퓨트 및 웹 서버 배포
  
  3. 접근 제어(보안 그룹)
  
  4. 권한(IAM) 최소권한
  
  5. 외부 접속 검증(택1)
  
  6. 운영 안정성(과금 방지)

</details>

<details>
  <summary>최종 결과물</summary>
  <img width="722" height="887" alt="스크린샷 2026-11-01 오후 4 13 31" src="https://github.com/user-attachments/assets/869c5ac9-0b98-453e-81d8-4783d41271fe" />
  
</details>

<details>
  <summary> 과제목표 및 제약사항 </summary>
  <img width="722" height="387" alt="스크린샷 2026-11-01 오후 4 11 37" src="https://github.com/user-attachments/assets/b10f293e-491a-4a29-bf29-07feb0a4975f" />
  
  <img width="722" height="1042" alt="스크린샷 2026-11-01 오후 4 10 24" src="https://github.com/user-attachments/assets/9f0f5ecb-5ab6-4860-9a5c-3e76f5fe3ab9" />

</details>
