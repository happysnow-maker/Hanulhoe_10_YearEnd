# 한울회 2026 정기총회 및 송년회 — 초대 메일 + 참석 회신

| 파일 | 용도 |
|---|---|
| `index.html` | 메일 본문 겸 웹 버전 (GitHub Pages) |
| `images/hero.gif`, `images/marquee.gif`, `images/mystery.gif` | 크리스마스 마을 배너 / 눈사람 LED 전광판 / 시크릿 선물 |
| `apps_script/Code.gs` | 응답 수집(doGet/doPost) + 초대·리마인더 메일 발송 |
| `tools/make_gifs.py` | GIF 재생성 스크립트 (문구 수정 후 `python tools/make_gifs.py`) |
| `share/` | 공유용 미리보기(회신 폼 비활성화) — 저장소에 올리지 않음 |
| `_preview.html` | 로컬 미리보기 전용 — 저장소에 올리지 않음 |

## 경품 긁기 동작
- 메일(Gmail 웹, Apple 메일 등 PC): 은박 카드에 마우스를 올리면 벗겨지며 경품 공개
- 휴대폰 메일 앱 / 스타일을 지우는 메일 앱: 은박 없이 경품이 바로 보임
- 웹 버전: 마우스나 손가락으로 은박을 직접 긁어서 공개

## 연결 정보
- 웹 페이지(GitHub Pages): https://happysnow-maker.github.io/Hanulhoe_10_YearEnd/ — 저장소 `happysnow-maker/Hanulhoe_10_YearEnd`
- 응답 스프레드시트 「한울회 2026 송년회 응답」: https://drive.google.com/open?id=1Jzv1xwSGoWYb8pxDcd7dNLk4JXFZZeQGHWtZjLEhP8g
- Apps Script(위 시트에 연결, happysnow@hanyang.ac.kr 소유): https://script.google.com/d/1kNMy9U87hhqqvvFaLiDuKaQQ37H4NM5cX290b1Gz3ZZvfKfhsZuHKnCm/edit
- 웹앱(회신 카드 제출 주소): `https://script.google.com/macros/s/AKfycbyXlp68exXGGvA5yIy_M9yU_3msr-IBGQCzCTM0FhiYxkZUXO5rb1GmWcmvlAPJS8Zhdw/exec`
- `apps_script/`는 clasp로 관리: `clasp --user hanulhoe push` 후 기존 배포를 새 버전으로 갱신
  `clasp --user hanulhoe update-deployment AKfycbyXlp68exXGGvA5yIy_M9yU_3msr-IBGQCzCTM0FhiYxkZUXO5rb1GmWcmvlAPJS8Zhdw` (URL 유지)

## 발송 순서
1. (최초 1회) Apps Script 편집기에서 `sendTest` 실행 → 권한 승인 → 내 메일함에서 확인(폼 제출까지 테스트)
2. 스프레드시트에 `명단` 시트 생성: A 성명 · B 이메일 · C 캠퍼스(선택) · D 소속(선택)
3. `sendInvitations` 실행 → E열에 발송 결과 기록
4. 11월 초 `sendReminderToNonResponders`로 미응답자에게 리마인더
5. 마감 후 후속 메일(`apps_script/Followup.gs`): `sendFollowupTests` → `previewFollowupTargets` →
   `sendExtensionNotice`(미회신·불참자에게 11/17(화)까지 연장 안내) · `sendThanksToAttendees`(참석자 감사) — 기록은 명단의 「연장안내 발송」「감사메일 발송」 열(없으면 맨 끝에 생성)
6. `index.html`·`images/` 수정 시 GitHub에 다시 올려야 메일·웹에 반영됨
7. D-2 메일(`apps_script/Reminder.gs`): `sendRemindTests` → `previewRemindTargets` →
   `sendRemindToAttendees`(참석자 리마인드 · 장소 주의) · `sendLastCallToOthers`(불참·미회신자 마지막 초대) — 기록은 명단의 「리마인드 발송」「마지막초대 발송」 열

## 11/25 송년의 밤 당일 진행
| 파일 | 용도 |
|---|---|
| `event_night.html` | 무대 진행 화면(16:9 슬라이드) — 표지 → 식순 → 순서별 화면, 사업보고·회장 선출·경품 추첨·기증자 촬영 연결 |
| `vote.html` | 참석자 휴대폰용 회장 후보 추천·투표 (QR) — GitHub Pages에 올라가 있어야 QR이 동작 |
| `event_print.html` | A4 1장 = A5 식순 2부 인쇄용 (여백 없음 · 배경 그래픽 켜기) |
| `report/` | 사업보고 PDF를 이미지로 변환한 것 (`tools/report_to_images.py`) — 행사용으로 임시 공개, 행사 후 내릴 예정 |
| `images/donor/` | 기증자 배너 (총장님 · 연구부총장님 · 공과대학장님_변중무 · 산단장님_강현종) |
| `apps_script/Event.gs` | 추천·투표·참석자 명단 API (`doGet`에 `action` 파라미터가 있으면 처리) |

- 투표 API는 회신 폼과 **별도 배포**: `https://script.google.com/macros/s/AKfycbzXL3KEjGZkIJPbCzCOaVViSlhsfw-ZXD_N_VG9bIexXPWnYCHa9p14g_OgXdjm8bkQCw/exec`
  Event.gs 수정 후: `clasp --user hanulhoe push` → `clasp --user hanulhoe update-deployment AKfycbzXL3KEjGZkIJPbCzCOaVViSlhsfw-ZXD_N_VG9bIexXPWnYCHa9p14g_OgXdjm8bkQCw`
- 관리자 키는 `apps_script/Event.gs`의 `EVENT.ADMIN_KEY` — 진행 화면 ⚙ 설정에 한 번 입력
- 조작: → / PageDown / Space 다음 · ← 이전 · Enter 연결 자료 · Esc 식순으로 · F 전체화면 · 경품 화면에서 Space = 한 명 추첨
- 리허설 후 ⚙ 설정 → 「경품 추첨 기록 초기화」「회장 추천·투표 초기화」
