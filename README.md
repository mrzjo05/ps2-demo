# PS2 demo — iToF × stereo RGB (Lichtblick web)

**보기:** https://mrzjo05.github.io/ps2-demo/

센서 녹화본(MCAP)을 브라우저의 Lichtblick 에서 재생한다. 설치할 것은 없다.

- 아래 ▶ 를 누르면 재생한다(반복 재생이 켜져 있다).
- **라이브** 탭: 스테레오 카메라 두 대(iToF 점을 겹쳐 그림), iToF depth, 공용 PTP 시간축 동기 표, IMU·마이크 그래프, 이벤트.
- **3D 클라우드** 탭: 스테레오 RGB 점구름과 iToF 점구름(청록)을 한 좌표계에 겹친다. 마우스로 돌리고(왼쪽 드래그) 옮기고(오른쪽 드래그) 확대한다(휠).
- 마이크 소리는 오디오 패널의 "소리 켜기" 를 눌러야 나온다(브라우저 정책).
- Chrome·Edge 를 권한다(H.264 를 WebCodecs 로 푼다).

## 들어 있는 것

| 경로 | 내용 |
|---|---|
| `index.html` | 입구 — 머리줄(로고·telelian.com 링크) 아래에 `app/` 을 띄우고 녹화본·레이아웃을 넘긴다 |
| `assets/telelian-logo.png` | 로고 |
| `app/` | Lichtblick 웹판 빌드 |
| `app/extensions/` | 시작할 때 읽어 들이는 확장: Cloudini(압축 점구름 풀기), 시연용 패널(동기 표·이벤트·오디오) |
| `data/` | 녹화본(MCAP, 약 10 초) — 점구름은 Cloudini 5 mm 압축. GitHub Pages 는 이 파일을 gzip 으로 보내 Range 조각이 깨지므로, 앱은 같은 파일을 raw.githubusercontent.com 에서 읽는다 |
| `layouts/PS2-Demo-v2.json` | 화면 배치 |

## 소스와 라이선스

- **Lichtblick**(MPL-2.0): https://github.com/lichtblick-suite/lichtblick v1.29.1 바탕. 수정본은 https://github.com/mrzjo05/lichtblick 브랜치 `hsb/1.29.1-web-demo`(37c01b24 = `hsb/1.29.1-hsb.3` c091044d + `source/lichtblick-bundled-extensions.patch`)이고 `yarn web:build:prod` 로 빌드했다.
  - 더한 것: 사이트에 둔 `.foxe` 를 읽기 전용으로 불러오는 확장 로더, 기본 어두운 테마, Accept-Ranges 를 노출하지 않는 서버(raw.githubusercontent.com)는 1 바이트 Range 요청으로 확인.
  - 라이선스 전문 `LICENSES/lichtblick.MPL-2.0.txt`.
- **Cloudini Foxglove 변환 확장**: 확장 코드 MIT(`LICENSES/cloudini-foxglove-cloudini-converter.MIT.txt`), 안의 Cloudini 라이브러리 Apache-2.0(`LICENSES/cloudini.Apache-2.0.txt`). 출처 https://github.com/facontidavide/cloudini/releases/tag/1.3.1
- **시연용 패널 확장(`hsb-panels.foxe`)과 녹화 데이터**: Telelian. 이 시연을 보는 용도로만 공개한다.
