# 출시 가이드

## 처음 한 번만 하는 준비

이 단계를 끝내야 자동 출시가 돌아갑니다. 비밀 값(토큰, 키)은 채팅에 붙여넣지 않습니다.

| # | 할 일 | 어디서 | 비용 |
|---|---|---|---|
| 1 | Expo 계정 만들기 | expo.dev | 무료 (무료 요금제는 월 빌드 수 제한 있음) |
| 2 | `cd mobile && npx eas-cli@latest init` 실행 → `app.json`에 `projectId`가 생김 → 커밋 | 내 PC 또는 이 저장소 | - |
| 3 | Expo 액세스 토큰 발급 → GitHub 저장소 Settings → Secrets → Actions에 `EXPO_TOKEN`으로 저장 | expo.dev 계정 설정 | - |
| 4 | Google Play 개발자 계정 만들기 | play.google.com/console | 1회 25달러 |
| 5 | Play Console에서 앱 만들기 (패키지 이름 `com.wook673.yeopker`) | Play Console | - |
| 6 | 첫 AAB는 손으로 올리기. Google이 첫 업로드는 API로 받지 않음. `npx eas-cli build -p android --profile production`로 만든 파일을 내부 테스트 트랙에 올림 | Play Console | - |
| 7 | Google 서비스 계정 JSON 키 만들기 → `npx eas-cli credentials`로 EAS에 등록 | Google Cloud + EAS | - |
| 8 | Apple Developer Program 가입 | developer.apple.com | 연 99달러 |
| 9 | `npx eas-cli build -p ios --profile production`을 한 번 직접 실행. Apple 로그인 후 인증서와 App Store Connect API 키를 EAS가 만들어 저장함 | 내 PC | - |

참고: 2023년 이후 만든 **개인** Play 개발자 계정은, 정식 출시 전에 비공개 테스트(테스터 12명, 14일)를 거쳐야 합니다. 정확한 조건은 Play Console에서 확인하세요.

## 출시 흐름 (준비 후 매번)

1. `release-manager` 에이전트에게 "1.1.0 출시해줘"라고 말합니다.
2. 에이전트가 버전을 올리고 PR을 엽니다.
3. 사람이 PR을 합칩니다.
4. 에이전트가 사용자 확인을 받고 `v1.1.0` 태그를 올립니다.
5. GitHub Actions `Mobile Release`가 EAS에서 안드로이드·iOS를 빌드하고 스토어에 보냅니다.
   - 안드로이드 → Play Console 내부 테스트 트랙 (초안)
   - iOS → TestFlight
6. 사람이 테스트 후 직접 공개합니다.
   - 안드로이드: Play Console에서 프로덕션으로 승격
   - iOS: App Store Connect에서 심사 제출

손으로 돌리려면: GitHub → Actions → Mobile Release → Run workflow.

## 테스트용 APK만 필요할 때

`npx eas-cli build -p android --profile preview` → 설치 링크가 나옵니다. 스토어를 거치지 않습니다.
