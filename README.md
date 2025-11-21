# RoadKeeper

로드킬 대시보드

## 📋 개요

RoadKeeper는 도로 위 사고로 인한 야생동물 사망(로드킬) 데이터를 시각화하고 분석하기 위한 대시보드 애플리케이션입니다.

* 발생 위치, 시간, 동물종, 사고 유형 등의 데이터를 지도 위에 표시하여 한눈에 파악할 수 있습니다.
* Streamlit을 이용한 웹 대시보드 형태로 구현되어 있어 사용이 간편합니다.
* YOLO(객체탐지) 및 지리공간 라이브러리(예: Leaflet) 등을 활용하여 데이터 수집·처리부터 시각화까지 통합적으로 다룹니다.

## 🧭 주요 기능

* 지도 표시: 사고 발생 지점을 지도 상에 마커/히트맵 형태로 시각화.
* 필터링: 동물종, 시간대, 지역 구분 등에 따른 필터 적용 가능.
* 상세 분석: 시간 흐름에 따른 사고 빈도 변화, 지역별 사고 밀도 비교 등.
* 데이터베이스 연동: MySQL 등을 통한 사고 데이터 저장 및 조회.
* 자동 탐지: YOLO 기반 모델(yolov8n.pt 등)을 활용해 영상/사진에서 로드킬 이벤트를 자동으로 분류·탐지.

## 🏗️ 프로젝트 구조

```
├── .vscode/  
├── app/             ← 대시보드 애플리케이션 코드  
├── data/            ← 원본 및 전처리된 데이터 파일  
├── mapdata/         ← 지도 시각화용 데이터(geojson 등)  
├── .gitattributes  
├── .gitignore  
├── README.md        ← 이 문서  
├── requirements.txt ← 필요한 Python 패키지 목록  
├── yolov8n.pt       ← YOLOv8 모델 가중치 파일  
└── yolo11n.pt       ← YOLO v11(?) 모델 가중치 파일  
```

## 🛠️ 설치 및 실행 방법

1. 저장소를 클론합니다.

   ```bash
   git clone https://github.com/toto6343/roadkeeper.git
   ```
2. 가상환경(venv 등)을 설정하고 활성화합니다.

   ```bash
   python -m venv venv  
   source venv/bin/activate   # Linux/Mac  
   .\venv\Scripts\activate    # Windows  
   ```
3. 필요 패키지를 설치합니다.

   ```bash
   pip install -r requirements.txt
   ```
4. 데이터베이스(MySQL)를 설정하고, `data/` 폴더의 데이터를 DB에 로드합니다.
   (DB 설정, 사용자/비밀번호, 스키마 등은 `app/config.py` 등에 정의되어야 합니다.)
5. 대시보드 앱을 실행합니다.

   ```bash
   streamlit run app/main.py
   ```
6. 브라우저에서 `http://localhost:8501` (기본)로 접속하여 대시보드를 확인합니다.

## 📂 데이터 정보

* 데이터 출처: 2025년 국토교통 데이터활용 경진대회 제공 데이터.
* 구조 예시:

  * `incident_id`: 사고 고유번호
  * `species`: 동물종명
  * `date_time`: 사고 발생 일시
  * `latitude`, `longitude`: 사고 위치 좌표
  * `road_type`: 도로 유형
  * `image_path`: 사고 사진 파일 경로(탐지 모델 입력용)
* 지도 시각화를 위해 `mapdata/` 폴더 내 GeoJSON 또는 Shapefile을 활용합니다.

## 🤖 객체 탐지 모델

* `yolov8n.pt`, `yolo11n.pt` 파일은 각각 YOLO v8, v11 계열의 가중치입니다.
* 사진/영상에서 동물 로드킬을 탐지하기 위해 사용됩니다.
* 사용자 필요에 따라 모델을 재학습하거나 개선할 수 있습니다.

## 🎯 활용 및 기대 효과

* 교통/도로 관련 기관에서 로드킬 사고 다발 지역을 파악하고 예방 대책 수립 가능.
* 환경 보호 및 생태계 보존 측면에서 동물 이동 경로 및 위험 구역 모니터링.
* 데이터 시각화 및 객체탐지 기술을 융합한 실증 사례로 활용 가능.

## ✅ 시작 가이드

* 대시보드 접속 후: 좌측 필터 메뉴에서 동물종 → 지역 → 시간대를 선택하여 지도 및 통계 변화를 확인하세요.
* ‘히트맵’ 또는 ‘마커’ 탭을 전환하면 사고 밀도·분포를 다른 시각으로 확인할 수 있습니다.
* 탐지 이미지 업로드 기능(추후 포함 예정)을 통해 실제 사진을 분석하고 예측 결과를 확인해보세요.

## 💡 향후 계획

* 실시간 탐지/알림 기능 추가: CCTV나 CCTV급 캠으로부터 실시간 로드킬 탐지 및 알림.
* 모바일 친화적 UI 제공: 도로 관리자 및 환경 조사원이 현장에서도 사용 가능하도록 앱/반응형 웹 지원.
* 머신러닝 기반 사고 예측 모델 개발: 사고 다발시점/고위험지역을 사전 예측.
* 동물종 및 도로 특성 데이터 보완: 보다 정밀한 분류 및 분석 가능.

## 📄 라이선스

본 프로젝트는 자유롭게 사용/수정/배포 가능합니다. 다만 출처 표기 및 본인의 책임 하에 사용되어야 합니다.

## 🙋 기여 방법

1. 이 저장소를 포크하세요.
2. 기능 개선이나 버그 수정을 위한 브랜치를 만드세요.
3. 변경사항을 커밋하고 푸시하세요.
4. 풀 리퀘스트(PR)를 생성하고 변경사항을 설명하세요.

## 🖼️ 스크린샷

![로드킬 발생위치](https://github.com/user-attachments/assets/e709a970-6983-4a2f-b301-8f7af9a52303)
![Image](https://github.com/user-attachments/assets/4f27f937-f4e0-4728-ab5c-7ab45c2f1a03)
![Image](https://github.com/user-attachments/assets/fdd78282-5a41-48d1-ac1f-b1bf5c0ef005)
![Image](https://github.com/user-attachments/assets/9bd2606f-0e7c-4039-a8cd-16e0c8abe065)
![Image](https://github.com/user-attachments/assets/800b4b29-f69b-4487-b56d-ec44b58c65c2)
![Image](https://github.com/user-attachments/assets/330d5a77-dceb-4857-8af6-15faabfd0950)
![Image](https://github.com/user-attachments/assets/445bc734-a404-40b6-be34-b0db940e3c0e)
![Image](https://github.com/user-attachments/assets/dde9f8a9-0340-459b-83a7-342265523e74)
![Image](https://github.com/user-attachments/assets/a7cc66ca-ed06-4a44-b16a-db158a95eaab)
![Image](https://github.com/user-attachments/assets/77f70d6a-fcb4-4d1d-a484-e48b459ef726)
![Image](https://github.com/user-attachments/assets/a98f27ec-9ec6-4e62-bba9-ea1a6dff59ef)
![Image](https://github.com/user-attachments/assets/8936a940-7475-472e-a957-15c15039e12b)

## 📞 문의

프로젝트 관련 문의는 저장소의 이슈(Tab: *Issues*)로 남겨주시거나, 직접 연락하실 수 있는 메일 주소(README 상단에 기재 가능)를 통해 주세요.

---

필요하신 다른 섹션(예: 기술 스택, 스크린샷 삽입, API 명세, 배포 가이드 등)을 추가하거나, 영문 버전으로 바꾸거나, 스타일을 다르게 하고 싶으시면 알려주세요!

---




