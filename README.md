# polymorph-maintenance

Polymorph 서비스 중단/접근불가 시 표시되는 정적 메인터넌스 페이지.

Cloudflare Worker가 origin(맥미니 k8s 클러스터)에서 5xx 응답을 감지하면 이 페이지의 HTML을 fetch해서 사용자에게 보여준다. 사용자의 브라우저 주소창은 원본 호스트(`*.polymorph.co.kr`)를 유지하므로, `index.html`의 client-side JS가 `window.location.host`를 읽어 해당 서비스 이름("집사요 점검 중" 등)으로 타이틀을 갱신한다.

## 호스팅

- GitHub Pages에서 직접 서빙: `https://polym-team.github.io/polymorph-maintenance/`
- Settings → Pages → Branch `main` / `/(root)`로 활성화
- 인프라/Cloudflare 자체 장애에도 GitHub Pages가 살아있는 한 동작 (의도된 독립성)

## 수정 시

- `index.html` 한 파일만 편집하면 끝. 빌드/CI 없음.
- 새 서비스 도메인 추가 시 `APP_NAMES` 객체에 한 줄 추가.
- 디자인 변경 시 `apps/maintenance`(k8s 클러스터 내부 점검 모드용 Next.js 앱)와 톤을 맞춰주면 좋다.
