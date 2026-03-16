# Vocfl - 가볍고 사용하기 쉬운 단어장 앱

Flutter로 개발된 개인용 단어장 애플리케이션입니다. 단어 세트를 관리하고, 플래시카드와 퀴즈로 학습할 수 있습니다.

## 주요 기능

- **단어 세트 관리** - 단어 세트를 생성, 수정, 삭제
- **단어 직접 입력** - 단어와 뜻을 직접 추가
- **CSV 가져오기** - CSV 파일로 단어 일괄 등록
- **플래시카드 학습** - 카드 형태로 단어 암기
- **단어 테스트** - 객관식 퀴즈로 실력 확인
- **학습 분석** - 맞힌 단어 / 틀린 단어 통계 확인
- **필터링** - 단어 세트를 조건에 맞게 필터링

## 기술 스택

- **Flutter** (Dart SDK `>=3.8.0`)
- **아키텍처** - Clean Architecture (Domain / Data / Presentation)
- **상태 관리** - Provider
- **DI** - get_it
- **로컬 DB** - sqflite
- **함수형** - dartz (Either 패턴)
- **CSV 처리** - csv + file_picker

## 프로젝트 구조

```
lib/
├── core/              # 공통 에러, 유스케이스 기반 클래스
├── main_init/         # 앱 초기화, 라우팅, DI, 테마
└── src/
    ├── data/          # 데이터소스, 모델, 리포지토리 구현체
    ├── domain/        # 엔티티, 리포지토리 인터페이스, 유스케이스
    └── presentation/  # 페이지, 위젯, 프로바이더
```

## 실행 방법

```bash
# 의존성 설치
flutter pub get

# 앱 실행
flutter run
```

## 지원 플랫폼

Android / iOS / Windows / macOS / Linux / Web

---

## 현재 상태

### 완성된 기능 ✅

| 기능 | 설명 |
|------|------|
| HomeView | 단어장 목록 표시, 필터링, 네비게이션 |
| WordsSetScreen | 단어장 상세 보기, 단어 미리보기 |
| FlashCard | 플래시카드 학습 (앞/뒤 전환, 이전/다음) |
| WordTestView | 4지선다형 퀴즈, 정답/오답 추적 |
| ResultView | 시험 결과 표시 및 분석 데이터 저장 |
| AddDirectView | 단어 직접 추가 |
| AddImportView | CSV 파일 가져오기 |
| SettingScreen | 기본 설정 화면 |

### 미완성 / 부분 구현 ⚠️

- **AnalysisView** - 분석 UI가 하드코딩된 테스트 상태. 실제 통계 시각화 없음
- **Drawer 라우팅** - "학습 분석" 메뉴가 AnalysisView가 아닌 SettingScreen으로 잘못 연결됨
- **단어 수정** - 기존 단어 수정 시 일부 UI가 빈 위젯(`Row()`) 반환
- **ResultView 버튼** - 하단 버튼 `onPressed: () {}` (미구현)

---

## 보완해야 할 사항

### 🔴 버그 (즉시 수정 필요)

1. **return 누락** - `WordTestView`, `FlashCard`에서 Failure 상태일 때 `return` 없이 `FailedScreen`을 생성만 하고 이후 코드가 계속 실행됨
2. **하드코딩 버그** - `MultipleWordsSetModel.toJson()`에서 `title: 'title'`로 하드코딩되어 저장 시 제목이 항상 'title'로 덮어씌워짐
3. **논리 오류** - `AnalysisProvider.deleteWrongWord()` / `deleteRightWord()`에서 조건이 반대로 작성됨 (`contains`가 false일 때 `removeWhere` 실행)
4. **await 누락** - `LocalDataSourceImpl.writeMultipleWordsSetsToLocalDataSource()`에서 파일 쓰기 시 `await` 없음

### 🟡 에러 처리 보강

- Consumer 빌더에서 에러 상태 반환 누락 다수 존재
- CSV 가져오기 시 파일 포맷 검증 없음
- 파일 I/O 실패 (권한 오류, 파일 없음) 처리 없음

### 🟡 코드 품질

- `print()` 문 7개 (프로덕션 코드에서 제거 필요)
- 매직 넘버 다수 (`height * 0.4`, `height * 0.818` 등) → 상수로 추출 필요
- 파일명 / 변수명 명명규칙 불일치 (snake_case vs camelCase 혼재)
- 긴 메서드 (`bodyBuilder`, `viewbuilder` 등이 150줄 이상)
- `mocktail` 패키지가 포함되어 있으나 테스트 코드 없음

### 🟢 개선 사항 (낮은 우선순위)

- 테스트 코드 작성 (현재 커버리지 거의 0%)
- AnalysisView 실제 데이터 연동 및 시각화
- 다국어(i18n) 지원
- 학습 분석 라우팅 수정
- 상수 파일 분리 (theme, strings 등)
