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

## 현재 상태

개발 중지 상태입니다.
