<img width="180" height="180" alt="image" src="https://github.com/user-attachments/assets/5287846f-eb19-4aa9-aaa2-80f3f47a7f29" />


# Safe

<aside>

### 앱 이름

- Safe(세잎)

---

### 앱 소개

- AI를 이용한 근로자 자세평가 및 안전장비 착용유무 탐지 앱

---

### 앱 목적

- 근로자의 자세평가 및 안전장비 착용여부를 탐지함으로써 근로자의 안전을 보장

---

### 개발기간
- 2025.07.21 ~2025.08.19 MVP 구현
- 2026.03.10 핵심기능만 탑재된 버전 앱스토어 배포
  
---

### 개발인원
- 2명

<table>
  <tr>
    <td align="center">
      <img src="https://avatars.githubusercontent.com/ChanSolShin" width="100"/><br/>
      <b>ChanSolShin</b>
    </td>
    <td align="center">
      <img src="https://avatars.githubusercontent.com/HunCY5" width="100"/><br/>
      <b>HunCY5</b>
    </td>
  </tr>
</table>

---

### 앱스토어 링크
https://apps.apple.com/us/app/%EC%84%B8%EC%9E%8E/id6759786625?l=ko

### 주요 기능

1. 근로자 자세평가 기능( RULA & REBA & OWAS )
2. 근로자 안전방지 착용여부 탐지기능( 안전모 & 안전조끼 )
3. 개선 필요 자세 및 안전장비 미착용 시, 위험로그 기록 기능
    - 자세평가: 일정 시간 동안 신체 각도 수집 후 평가하여 위험 자세일 경우 기록
    - 안전장비: 일정 시간 동안 헬멧, 안전조끼 중 하나라도 미착용 시 기록
    - 기록 내용: 날짜, 구역, 자세평가 or 안전장비 구분, 자세평가 점수, 스크린샷
    
4. 앱스토어 배포된 버전은 로그 기록등을 제외한 자세평가 및 안전장비 착용 탐지 기능만 탑재후 배포
</aside>

### 사용기술

- **Language:** Swift
- **Framework:** UIKit
- **Architecture:** MVC
- **Backend:** Firebase (Firestore, Authentication)
- **Asynchronous:**  Combine
- **Version Control:** Git & GitHub
- **Collaboration**: Notion
- **CNN Model: YOLOv11, MoveNet**
---
## 아키텍처

safe는 UIKit 기반의 MVC 구조로 구성되어 있습니다.

화면 단위 기능은 `ViewController` 하위에 분리되어 있으며, 각 화면의 UI는 `View` 계층에서 관리합니다.  
사용자 인증, 근로자 관리, 위험 로그 조회는 Firebase Auth와 Firestore를 사용하며, 실시간 위험 감지는 `Camera`, `ML`, `PPEDetection` 영역에서 처리합니다.

```text
safe/
├── App
│   ├── AppDelegate.swift                # Firebase 초기화 및 앱 생명주기 관리
│   ├── SceneDelegate.swift              # Window 생성, 초기 화면 및 로그인 상태 라우팅
│   └── MainTabBarController.swift       # 안전감시/위험로그/근로자/프로필 탭 구성
│
├── ViewController
│   ├── Login
│   │   ├── ChoiceLoginViewController.swift       # 근로자/관리자 로그인 선택
│   │   ├── CrewLoginViewController.swift         # 근로자 로그인 처리
│   │   └── ManagerLoginViewController.swift      # 관리자 로그인 처리
│   │
│   ├── SignUp
│   │   ├── CrewSignUpViewController.swift        # 근로자 회원가입 처리
│   │   └── ManagerSignUpViewController.swift     # 관리자 회원가입 처리
│   │
│   ├── SafetyManager
│   │   └── SafetyManagerViewController.swift     # 안전 감시 메인 화면 및 위험 감지 진입
│   │
│   ├── RiskDetectionViewController.swift         # 카메라 기반 자세/PPE 위험 감지
│   ├── RiskLogViewController.swift               # 위험 로그 조회 및 상세 확인
│   ├── CrewManageViewController.swift            # 근로자 초대 및 관리
│   └── ProfileViewController.swift               # 프로필, 로그인/회원가입, 출퇴근 상태 관리
│
├── View
│   ├── Login
│   │   ├── ChoiceLoginView.swift                 # 로그인 선택 UI
│   │   ├── CrewLoginView.swift                   # 근로자 로그인 UI
│   │   └── ManagerLoginView.swift                # 관리자 로그인 UI
│   │
│   ├── SignUp
│   │   ├── CrewSignUpView.swift                  # 근로자 회원가입 UI
│   │   └── ManagerSignUpView.swift               # 관리자 회원가입 UI
│   │
│   ├── CrewManageView.swift                      # 근로자 관리 화면 UI
│   ├── CrewRowView.swift                         # 근로자 목록 셀 UI
│   ├── CurrentCrewView.swift                     # 현재 근로자 정보 UI
│   ├── RegisterCrewView.swift                    # 근로자 등록/초대 UI
│   ├── CrewMessageView.swift                     # 근로자 메시지 UI
│   ├── ProfileView.swift                         # 프로필 화면 UI
│   ├── RiskLogView.swift                         # 위험 로그 목록 UI
│   ├── RiskLogCardView.swift                     # 위험 로그 카드 UI
│   └── PPEDetectionOverlayView.swift             # PPE 감지 결과 오버레이 UI
│
├── Model
│   ├── CrewLoginModel.swift                      # 근로자 로그인 데이터 모델
│   ├── CrewSignUpModel.swift                     # 근로자 회원가입 데이터 모델
│   ├── ManagerLoginModel.swift                   # 관리자 로그인 데이터 모델
│   ├── ManagerSignUpModel.swift                  # 관리자 회원가입 데이터 모델
│   │
│   └── PPEDetection
│       ├── PPEDetectionModel.swift               # PPE 감지 결과 모델
│       ├── PPEDetector.swift                     # YOLO/CoreML 기반 PPE 감지 처리
│       └── PPERiskLogger.swift                   # PPE 위험 로그 저장
│
├── Camera
│   └── CameraFeedManager.swift                   # 카메라 프레임 수집 및 감지 화면 전달
│
├── ML
│   ├── Extensions
│   │   ├── CVPixelBuffer+TFLite.swift            # TensorFlow Lite 픽셀 버퍼 변환 확장
│   │   ├── CGSize+TFLite.swift                   # TensorFlow Lite 크기 변환 확장
│   │   └── Data+TFLite.swift                     # TensorFlow Lite 데이터 변환 확장
│   │
│   └── Models
│       ├── PoseEstimator.swift                   # 자세 추정 공통 인터페이스
│       ├── PoseNet.swift                         # PoseNet 기반 자세 추정
│       ├── MoveNet.swift                         # MoveNet 기반 자세 추정
│       ├── PoseConfig.swift                      # 자세 추정 설정값
│       ├── PoseData.swift                        # 자세 추정 결과 데이터
│       ├── PoseAngle.swift                       # 관절 각도 계산
│       ├── JointAngles.swift                     # 주요 관절 각도 모델
│       ├── TwistAndBending.swift                 # 비틀림/굽힘 자세 판단
│       ├── PostureEvaluatorBuffer.swift          # 자세 평가 버퍼
│       ├── PostureRiskLogger.swift               # 자세 위험 로그 저장
│       │
│       └── ErgonomicAssessment
│           ├── OWAS.swift                        # OWAS 작업 자세 평가
│           ├── REBA.swift                        # REBA 작업 자세 평가
│           └── RULA.swift                        # RULA 작업 자세 평가
│
├── Resources
│   ├── Assets.xcassets                           # 앱 아이콘, 로고, 카메라/PPE/경고 이미지
│   ├── GoogleService-Info.plist                  # Firebase 설정 파일
│   └── DetectionYolov11.mlpackage                # PPE 감지용 CoreML 모델
│
├── Tests
│   └── SafeTests.swift                           # Unit Test 코드
│
└── Project
    ├── Project.swift                             # Tuist 프로젝트 설정
    ├── Tuist.swift                               # Tuist 설정
    ├── Podfile                                  # CocoaPods 의존성 설정
    └── README.md                               # 프로젝트 설명 문서
```
---
## 배운점 및 성과

- 오픈소스 적용 및 올바른 라이선스 범위 학습
- 딥러닝 모델 학습 및 프로젝트 적용
- 서버기반으로 동작하는 타이머의 구현 방법(앱 종료시에도 작동)
- 서로 다른 CNN모델 통합 및 개선 된 프레임 처리 방법
- observe 패턴을 이용하여 다른부분의 동작을 감지하는 로직 작성

---
<p align="center">
  <img src="https://github.com/user-attachments/assets/ad376428-1880-495b-b740-2bad2c20a6c8" width="180"/>
  <img src="https://github.com/user-attachments/assets/7d336d63-7665-4793-ad62-979d4377aa61" width="180"/>
  <img src="https://github.com/user-attachments/assets/ea606746-6a00-45ad-bb3e-8b55c8bb5c70" width="180"/>
</p>
