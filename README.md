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

## 배운점 및 성과

- 오픈소스 적용 및 올바른 라이선스 범위 학습
- 딥러닝 모델 학습 및 프로젝트 적용
- 서버기반으로 동작하는 타이머의 구현 방법(앱 종료시에도 작동)
- 서로 다른 CNN모델 통합 및 개선 된 프레임 처리 방법
- observe 패턴을 이용하여 다른부분의 동작을 감지하는 로직 작성

---
<img width="300" height="2556" alt="image" src="https://github.com/user-attachments/assets/ad376428-1880-495b-b740-2bad2c20a6c8" />
<img width="300" height="2556" alt="image" src="https://github.com/user-attachments/assets/7d336d63-7665-4793-ad62-979d4377aa61" />
<img width="300" height="2556" alt="image" src="https://github.com/user-attachments/assets/ea606746-6a00-45ad-bb3e-8b55c8bb5c70" />

