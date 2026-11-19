# 잿빛 심연 (ASHEN ABYSS) — 앱 패키지

이 폴더 하나로 **안드로이드 앱(APK)** 과 **설치형 웹앱(PWA)** 을 모두 만들 수 있습니다.

```
app/
├─ www/                 ← 게임 본체(최적화 완료) + PWA 파일
│  ├─ index.html        (8.4MB, 그림·코드 압축)
│  ├─ manifest.webmanifest
│  ├─ sw.js             (오프라인 캐시)
│  └─ icons/
├─ android/             ← 안드로이드 스튜디오 프로젝트 (Capacitor 7)
├─ capacitor.config.json  (앱 ID: com.ashenabyss.game, 이름: 잿빛 심연)
└─ .github/workflows/build-apk.yml  (GitHub에서 APK 자동 빌드)
```

## 방법 A. 안드로이드 스튜디오로 APK 만들기
1. Node.js 20 이상, Android Studio(최신) 설치
2. 이 폴더에서 터미널 실행 → `npm install` → `npx cap sync android`
3. `npx cap open android` (또는 Android Studio에서 `android` 폴더 열기)
4. Gradle 동기화가 끝나면 메뉴 **Build → Build App Bundle(s) / APK(s) → Build APK(s)**
5. `android/app/build/outputs/apk/debug/app-debug.apk` 를 휴대폰에 설치

> 구글 플레이 출시용은 **Build → Generate Signed App Bundle** 로 서명 키를 만들어 `.aab` 를 생성하세요.

## 방법 B. GitHub에서 자동으로 APK 받기 (PC 설치 불필요)
1. 이 폴더를 GitHub 저장소로 올리기
2. 저장소 **Actions → 안드로이드 APK 빌드 → Run workflow**
3. 5~8분 후 완료된 실행의 **Artifacts → ashen-abyss-apk** 다운로드

## 방법 C. 설치형 웹앱(PWA)으로 배포
1. `www` 폴더를 Netlify Drop / GitHub Pages / Vercel 등 HTTPS 호스팅에 업로드
2. 휴대폰 브라우저로 접속 → **홈 화면에 추가** (안드로이드는 '앱 설치' 버튼)
3. 아이콘으로 실행하면 주소창 없는 전체화면, 한 번 실행 후엔 **오프라인에서도 실행**

## 앱 설정 요약
| 항목 | 값 |
|---|---|
| 화면 | 세로 고정, 전체화면(상태바·내비게이션바 숨김) |
| 저장 | 기기 내부 저장(localStorage) — 앱 삭제 시 진행도 삭제 |
| 아이콘/스플래시 | 붉은 달·기사 일러스트 |
| 게임 수정 반영 | 새 `index.html` 을 `www/` 에 덮어쓰고 `npx cap sync android` 후 다시 빌드 |
