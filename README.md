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

## 발송 순서
1. GitHub에 `Hanulhoe_10_YearEnd` 저장소를 만들고 `index.html`, `images/`를 올린 뒤 Pages 활성화
2. 기존 스프레드시트의 Apps Script에 `Code.gs` 붙여넣기 → **배포 관리 → 기존 배포 수정 → 새 버전** (URL 유지)
3. 스프레드시트에 `명단` 시트 생성: A 성명 · B 이메일 · C 캠퍼스(선택) · D 소속(선택)
4. `sendTest` 실행 → 내 메일함에서 확인(폼 제출까지 테스트)
5. `sendInvitations` 실행 → E열에 발송 결과 기록
6. 11월 초 `sendReminderToNonResponders`로 미응답자에게 리마인더
