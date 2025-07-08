# MealMate - 개인 맞춤형 식단 관리 및 칼로리 추적 Android 애플리케이션

## 🎯 프로젝트 개요

**MealMate**는 **개인의 신체 정보와 목표에 맞춘 과학적인 식단 관리**를 지원하는 Android 네이티브 애플리케이션입니다. **Harris-Benedict 공식**을 기반으로 한 정밀한 칼로리 계산과 **정부 공공 API**를 활용한 신뢰할 수 있는 영양 정보를 제공합니다.

### 📊 프로젝트 배경
- **현대인의 식습관 관리 어려움**: 바쁜 일상 속에서 체계적인 식단 관리의 필요성 증대
- **개인 맞춤형 칼로리 계산**: 성별, 나이, 활동량, 목표를 고려한 과학적 접근
- **신뢰할 수 있는 영양 정보**: 정부 공공 데이터 기반의 정확한 식품 영양 정보
- **일주일 단위 진행률 추적**: 지속적인 동기부여를 위한 시각적 피드백

### ✨ 핵심 기능 및 특징
- 🧮 **과학적 칼로리 계산**: Harris-Benedict 공식 기반 기초대사율(BMR) 산출
- 📱 **직관적인 UI/UX**: Material Design 기반의 사용자 친화적 인터페이스
- 📊 **실시간 데이터 시각화**: MPAndroidChart를 활용한 일주일 칼로리 달성률 차트
- 🗄️ **로컬 데이터베이스**: Room을 활용한 오프라인 데이터 관리
- 🌐 **공공 API 연동**: 정부 식품의약품안전처 영양성분 API 활용
- 🏗️ **현대적 아키텍처**: MVVM 패턴, Hilt 의존성 주입, DataBinding 적용

## 🔬 기술적 특징 및 아키텍처

### 🏛️ 아키텍처 패턴
```
📱 View Layer (Activity/Fragment)
    ↕️ DataBinding
🎮 ViewModel Layer (LiveData + Repository)
    ↕️ Dependency Injection (Hilt)
🗄️ Model Layer (Room Database + API)
```

### 🛠️ 기술 스택
- **언어**: Java 11
- **UI Framework**: Android SDK (API 24-33)
- **아키텍처**: MVVM Pattern + Repository Pattern
- **의존성 주입**: Dagger Hilt 2.44
- **데이터베이스**: Room 2.5.1 (SQLite 기반)
- **네트워킹**: Retrofit 2.9.0 + Gson Converter
- **차트**: MPAndroidChart v3.1.0
- **UI 컴포넌트**: Material CalendarView 1.4.3
- **빌드 도구**: Gradle, Android Studio

### 📐 핵심 비즈니스 로직

#### 🧮 Harris-Benedict 기초대사율 계산
```java
// 남성: BMR = (10 × 체중) + (6.25 × 키) - (5 × 나이) + 5
// 여성: BMR = (10 × 체중) + (6.25 × 키) - (5 × 나이) - 161

최종 칼로리 = BMR × 활동지수 × 목적지수
```

#### 📊 활동 지수 및 목적 지수
- **활동 지수**: 좌식(1.2) ~ 매우 활동적(1.9)
- **목적 지수**: 다이어트(0.8), 체중유지(1.0), 벌크업(1.2)

## 🚀 빠른 시작

### 1. 개발 환경 설정

```bash
# 필요 도구
- Android Studio Arctic Fox 이상
- JDK 11 이상
- Android SDK API 24-33
- Gradle 7.0 이상
```

### 2. 프로젝트 클론 및 설정

```bash
# 프로젝트 클론
git clone <repository-url>
cd MealMate

# Android Studio에서 프로젝트 열기
# File -> Open -> 프로젝트 폴더 선택
```

### 3. 빌드 및 실행

```bash
# Gradle 동기화 후 빌드
./gradlew build

# 디바이스/에뮬레이터에 설치
./gradlew installDebug
```

## 📱 주요 화면 및 기능

### 🏠 홈 화면 (HomeFragment)
```
📊 사용자 맞춤 정보
├── 👤 사용자명 + 목적 (다이어트/벌크업/체중유지)
├── ⚖️ 현재 체중 / 목표 체중
└── 📈 일주일 칼로리 달성률 차트

📝 오늘의 식단
├── ☀️ 아침식사 체크리스트
├── 🌅 점심식사 체크리스트
└── 🌙 저녁식사 체크리스트
```

### 📅 달력 화면 (CalendarFragment)
- **Material CalendarView**: 날짜별 식단 기록 조회
- **월간 뷰**: 식단 완료 여부 시각적 표시
- **날짜 선택**: 특정 날짜 식단 상세 보기

### 🍎 음식 검색 화면 (FoodFragment)
- **실시간 검색**: 정부 API 기반 음식 검색
- **영양 정보**: 칼로리, 탄수화물, 단백질, 지방 정보
- **즐겨찾기**: 자주 먹는 음식 저장 기능

### 👤 사용자 설정 화면 (UserFragment)
- **개인 정보 관리**: 키, 몸무게, 나이, 성별 수정
- **목표 설정**: 다이어트/벌크업/체중유지 선택
- **활동량 설정**: 5단계 활동 수준 선택

## 🗄️ 데이터베이스 스키마

### 📊 주요 엔티티

#### 👤 User 테이블
```sql
CREATE TABLE user (
    userIndex INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    height REAL,
    weight REAL,
    targetWeight REAL,
    age INTEGER,
    gender INTEGER,        -- 1: 남성, 2: 여성
    activityLevel INTEGER, -- 1-5: 좌식~매우활동적
    purpose INTEGER,       -- 1: 다이어트, 2: 벌크업, 3: 체중유지
    bmr REAL              -- 계산된 기초대사율
);
```

#### 🍽️ Meal 테이블
```sql
CREATE TABLE meal (
    mealIndex INTEGER PRIMARY KEY AUTOINCREMENT,
    mealDate TEXT NOT NULL,
    mealCnt INTEGER,       -- 식사 번호 (1: 아침, 2: 점심, 3: 저녁)
    checked INTEGER,       -- 0: 미완료, 1: 완료
    mealPreset TEXT        -- 프리셋 이름
);
```

#### 🥗 Food 테이블
```sql
CREATE TABLE food (
    foodIndex INTEGER PRIMARY KEY AUTOINCREMENT,
    foodName TEXT NOT NULL,
    food1serving REAL,     -- 1회 제공량(g)
    foodKcal REAL,         -- 칼로리(kcal)
    foodCarbohydrates REAL, -- 탄수화물(g)
    foodProtein REAL,      -- 단백질(g)
    foodFat REAL,          -- 지방(g)
    food_company TEXT,     -- 제조사/구분
    foodLike INTEGER       -- 0: 일반, 1: 즐겨찾기
);
```

## 🌐 API 연동

### 🏛️ 식품의약품안전처 영양성분 API
```java
Base URL: http://apis.data.go.kr/1471000/FoodNtrIrdntInfoService1/
Endpoint: getFoodNtrItdntList1

Parameters:
- serviceKey: 인증키
- desc_kor: 식품명 (한글)
- type: json (응답 형식)
```

### 📦 API 응답 데이터 구조
```json
{
  "header": {
    "resultCode": "00",
    "resultMsg": "NORMAL SERVICE."
  },
  "body": {
    "totalCount": 1,
    "items": [{
      "DESC_KOR": "쌀밥",
      "SERVING_WT": 210.0,
      "NUTR_CONT1": 310.0,  // 칼로리
      "NUTR_CONT2": 68.9,   // 탄수화물
      "NUTR_CONT3": 6.5,    // 단백질
      "NUTR_CONT4": 0.6     // 지방
    }]
  }
}
```

## 🎨 UI/UX 디자인 철학

### 🎯 디자인 원칙
1. **직관성**: 복잡한 기능을 단순하고 명확하게 표현
2. **일관성**: Material Design 가이드라인 준수
3. **접근성**: 모든 연령대가 쉽게 사용할 수 있는 인터페이스
4. **피드백**: 사용자 행동에 대한 즉각적인 시각적 피드백

### 🎨 색상 체계
```xml
<!-- Primary Colors -->
<color name="orange">#FF8C00</color>
<color name="white">#FFFFFF</color>
<color name="trans">#F5F5F5</color>

<!-- Semantic Colors -->
<color name="black_40">#666666</color>
<color name="success">#4CAF50</color>
<color name="warning">#FF9800</color>
```

### 📱 반응형 레이아웃
- **다양한 화면 크기 지원**: 스마트폰, 태블릿 대응
- **적응형 UI**: 세로/가로 화면 모드 자동 조정
- **터치 친화적**: 최소 48dp 터치 영역 보장

## 📊 성능 최적화

### 🚀 성능 향상 기법
1. **LazyLoading**: RecyclerView를 통한 효율적인 리스트 렌더링
2. **데이터 캐싱**: Room을 활용한 로컬 데이터 캐싱
3. **이미지 최적화**: Vector Drawable 사용으로 다해상도 지원
4. **메모리 관리**: ViewModel + LiveData로 메모리 누수 방지

### 📈 앱 크기 최적화
```
APK Size: ~8MB (최적화 후)
- ProGuard 적용으로 코드 난독화 및 크기 축소
- 미사용 리소스 제거
- Vector Drawable 활용
```

## 🧪 테스트 전략

### 🔍 테스트 구조
```
src/test/               # 단위 테스트
├── ExampleUnitTest.java
└── model/
    └── BenedictCalculatorTest.java

src/androidTest/        # 계측 테스트
├── ExampleInstrumentedTest.java
└── database/
    └── DatabaseTest.java
```

### ✅ 주요 테스트 케이스
- **칼로리 계산 정확성**: Benedict 공식 계산 검증
- **데이터베이스 CRUD**: Room 데이터베이스 연산 테스트
- **API 통신**: Retrofit 네트워크 호출 테스트
- **UI 상호작용**: Espresso를 활용한 UI 테스트

## 🛡️ 보안 및 개인정보 보호

### 🔒 보안 조치
- **로컬 데이터 저장**: 개인정보는 디바이스 내부에만 저장
- **API 키 보안**: Constants 클래스를 통한 민감 정보 관리
- **데이터 암호화**: Room 데이터베이스 SQLCipher 적용 가능
- **권한 최소화**: 필요한 권한만 요청 (INTERNET, ACCESS_NETWORK_STATE)

### 🛡️ 개인정보 처리 방침
```
수집 정보: 이름, 키, 몸무게, 나이, 성별
저장 위치: 사용자 디바이스 로컬 저장소
외부 전송: 없음 (모든 데이터는 로컬에서 처리)
데이터 삭제: 앱 제거 시 모든 데이터 자동 삭제
```

## 📁 프로젝트 구조

```
MealMate/
├── app/
│   ├── src/main/
│   │   ├── java/com/anonymous/mealmate/
│   │   │   ├── api/                    # 🌐 네트워크 API 레이어
│   │   │   │   ├── ChartApiHelper.java
│   │   │   │   └── FoodApiHelper.java
│   │   │   ├── constants/              # 📋 상수 정의
│   │   │   │   ├── Constants.java
│   │   │   │   └── UserHashMap.java
│   │   │   ├── feature/                # 🔧 핵심 비즈니스 로직
│   │   │   │   ├── BenedictCalculator.java
│   │   │   │   ├── Date.java
│   │   │   │   └── MealMateApplication.java
│   │   │   ├── model/                  # 📊 데이터 모델 레이어
│   │   │   │   ├── dao/               # 🗄️ 데이터베이스 접근 객체
│   │   │   │   ├── database/          # 🏗️ 데이터베이스 설정
│   │   │   │   ├── dto/               # 📦 데이터 전송 객체
│   │   │   │   ├── entity/            # 🏛️ 데이터베이스 엔티티
│   │   │   │   └── repository/        # 📚 데이터 저장소 패턴
│   │   │   ├── service/               # ⚙️ 서비스 레이어
│   │   │   ├── view/                  # 🎨 프레젠테이션 레이어
│   │   │   │   ├── activity/         # 📱 액티비티
│   │   │   │   ├── adapter/          # 🔄 어댑터 패턴
│   │   │   │   ├── dialog/           # 💬 다이얼로그
│   │   │   │   └── fragment/         # 🧩 프래그먼트
│   │   │   └── viewmodel/            # 🎮 뷰모델 (MVVM)
│   │   └── res/                      # 📱 리소스 파일
│   │       ├── drawable/             # 🎨 드로어블 리소스
│   │       ├── font/                 # 🔤 폰트 리소스
│   │       ├── layout/               # 📐 레이아웃 XML
│   │       ├── menu/                 # 📋 메뉴 리소스
│   │       ├── values/               # 💾 값 리소스
│   │       └── mipmap-*/             # 🖼️ 앱 아이콘
│   └── build.gradle                  # 🔧 모듈 빌드 설정
├── gradle/                           # 🛠️ Gradle 래퍼
├── build.gradle                      # 🏗️ 프로젝트 빌드 설정
├── settings.gradle                   # ⚙️ 프로젝트 설정
└── README.md                         # 📖 프로젝트 문서
```

## 📈 향후 개발 계획

### 🔄 기능 확장
- [ ] **소셜 기능**: 친구와 식단 공유 및 경쟁
- [ ] **AI 추천**: 머신러닝 기반 개인 맞춤 식단 추천
- [ ] **운동 연동**: 소모 칼로리 계산 및 통합 관리
- [ ] **영양사 상담**: 전문가 상담 서비스 연동

### 🌐 플랫폼 확장
- [ ] **iOS 버전**: Swift 기반 iOS 애플리케이션 개발
- [ ] **웹 애플리케이션**: React 기반 웹 버전 제공
- [ ] **백엔드 API**: Spring Boot 기반 클라우드 서비스

### 🚀 기술적 개선
- [ ] **Jetpack Compose**: 최신 UI 프레임워크 도입
- [ ] **Kotlin 마이그레이션**: 코틀린 언어로 점진적 전환
- [ ] **GraphQL**: 효율적인 데이터 쿼리 시스템
- [ ] **오프라인 우선**: Progressive Web App 기능

## 🔧 개발 환경 및 도구

### 🛠️ 개발 도구
```
IDE: Android Studio 2023.1.1+
언어: Java 11
빌드 도구: Gradle 8.0+
버전 관리: Git
의존성 관리: Gradle Dependency Management
```

### 📦 주요 라이브러리 버전
```gradle
// 핵심 Android
implementation 'androidx.appcompat:appcompat:1.6.1'
implementation 'com.google.android.material:material:1.9.0'

// 아키텍처 컴포넌트
implementation 'androidx.room:room-runtime:2.5.1'
implementation 'com.google.dagger:hilt-android:2.44'

// 네트워킹
implementation 'com.squareup.retrofit2:retrofit:2.9.0'
implementation 'com.squareup.retrofit2:converter-gson:2.9.0'

// UI 컴포넌트
implementation 'com.github.PhilJay:MPAndroidChart:v3.1.0'
implementation 'com.prolificinteractive:material-calendarview:1.4.3'
```

## 🚀 빌드 및 배포

### 🔨 빌드 명령어
```bash
# 디버그 빌드
./gradlew assembleDebug

# 릴리스 빌드
./gradlew assembleRelease

# 테스트 실행
./gradlew test
./gradlew connectedAndroidTest

# 정적 분석
./gradlew lint
```

### 📦 APK 생성
```bash
# 서명된 APK 생성
./gradlew assembleRelease

# APK 위치
app/build/outputs/apk/release/app-release.apk
```

## 🤝 기여 가이드라인

### 🌟 기여 방법
1. **이슈 등록**: 버그 리포트 또는 기능 제안
2. **포크**: 프로젝트를 개인 계정으로 포크
3. **브랜치 생성**: feature/기능명 또는 bugfix/버그명
4. **커밋**: 명확한 커밋 메시지 작성
5. **풀 리퀘스트**: 상세한 설명과 함께 PR 생성

### 📋 코딩 컨벤션
```java
// 클래스명: PascalCase
public class MealCheckViewModel { }

// 메서드명: camelCase
public void calculateBMR() { }

// 상수: UPPER_SNAKE_CASE
public static final int MEAL_BREAKFAST = 1;

// 변수명: camelCase
private User currentUser;
```

## 📞 프로젝트 정보

### 📚 참고 자료
- [Android Developer Documentation](https://developer.android.com/)
- [Material Design Guidelines](https://material.io/design)
- [Harris-Benedict Formula](https://en.wikipedia.org/wiki/Harris%E2%80%93Benedict_equation)
- [식품의약품안전처 공공데이터](https://www.data.go.kr/)

### 🏆 주요 성과
- ✅ **완전한 MVVM 아키텍처** 구현
- ✅ **과학적 칼로리 계산** 시스템 구축
- ✅ **정부 공공 API** 연동 성공
- ✅ **직관적인 UI/UX** 디자인 완성
- ✅ **로컬 데이터베이스** 최적화

---

**🎯 Project Goals**: 개인 맞춤형 식단 관리 → 건강한 라이프스타일 지원  
**🔑 Key Technologies**: Android Native, MVVM, Room Database, Retrofit API  
**📈 Impact**: 과학적 접근을 통한 체계적인 식단 관리 솔루션

**Made with ❤️ for Healthy Lifestyle Management** 
