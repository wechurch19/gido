# 우리는교회 · 그래서 기도

화면은 **GitHub Pages**, 데이터는 **구글 시트 + Apps Script** 에 저장하는 교회 기도 앱입니다.

```
index.html            ← 화면 (GitHub Pages가 서빙)
manifest.webmanifest  ← 홈 화면에 앱처럼 설치
icons/                ← 앱 아이콘 (svg, 192, 512, maskable, apple-touch, favicon)
apps-script/          ← 구글에 올리는 서버 코드 (Code.gs, appsscript.json)
```

## 1. 서버(Apps Script) 준비
1. 새 구글 시트를 만들고 **확장 프로그램 → Apps Script** 를 엽니다.
2. `apps-script/Code.gs` 내용을 붙여넣고, ⚙ 프로젝트 설정에서 "appsscript.json 표시"를 켠 뒤 `apps-script/appsscript.json` 도 붙여넣습니다.
   (이전에 만든 `index` HTML 파일이 있다면 삭제하세요. 더 이상 쓰지 않습니다.)
3. `setup` 함수를 한 번 **실행**해 권한을 승인합니다. (시트 탭 4개가 자동 생성됩니다)
4. **배포 → 새 배포 → 웹 앱** → 실행: **나** / 액세스: **모든 사용자** → 배포.
5. 나온 **웹 앱 URL(…/exec)** 을 복사합니다.

관리자 비밀번호는 시트 `설정` 탭 B2 (기본 7008, 숫자만).

## 2. 화면(GitHub Pages) 올리기
1. `index.html` 안의 `API_URL` 한 줄에 위 URL을 붙여넣습니다.
   ```js
   var API_URL = 'https://script.google.com/macros/s/XXXX/exec';
   ```
2. 이 폴더 전체를 GitHub 저장소에 올립니다.
3. 저장소 **Settings → Pages → Branch: `main` / 폴더: `/ (root)`** → Save.
4. 1~2분 뒤 `https://<계정>.github.io/<저장소>/` 가 앱 주소입니다. 이 주소를 성도들에게 공유하세요.

## 3. 폰에 앱처럼 설치
- 아이폰: Safari → 공유 → **홈 화면에 추가**
- 안드로이드: Chrome → 메뉴 → **앱 설치 / 홈 화면에 추가**

## 참고
- Apps Script 코드를 고친 뒤에는 **배포 → 배포 관리 → 새 버전** 으로 다시 배포해야 반영됩니다. (URL은 그대로)
- 화면만 고칠 때는 GitHub에 올리기만 하면 됩니다.
- 처음 열 때 지난번 데이터를 먼저 보여 주고 최신 데이터를 뒤에서 받아 오므로 체감 속도가 빠릅니다.
- Apps Script와 연동할 때 `clasp` 를 쓰고 싶다면 `.clasp.json` 에 `"rootDir": "apps-script"` 를 지정하세요. `.clasprc.json` 은 `.gitignore` 로 막혀 있습니다.
