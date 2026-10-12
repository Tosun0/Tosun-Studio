# Tosun Studio Git 배포

## 저장소 구성

- `.agents/plugins/marketplace.json`: Git 배포용 마켓플레이스
- `plugins/tosun-studio/`: Codex 플러그인 본체
- `plugins/tosun-studio/assets/`: composer 아이콘과 로고
- `plugins/tosun-studio/skills/00-master-tosun/SKILL.md`: 전체 워크플로우·승인 지침
- `plugins/tosun-studio/skills/{01-storyboard,02-image,03-video,04-remotion}/SKILL.md`: 시퀀스별 실행 지침

## 설치

Git 배포본을 설치합니다.

```powershell
codex plugin marketplace add https://github.com/Tosun0/Tosun-Studio.git
codex plugin add tosun-studio@tosun-team
```

## 업데이트와 적용 확인

1. 스킬을 수정한 배포는 `plugins/tosun-studio/.codex-plugin/plugin.json`의 버전을 올리고 검증 후 커밋·푸시합니다.
2. 해당 마켓플레이스만 갱신한 뒤 플러그인을 설치합니다. 다른 플러그인을 일괄 갱신하거나 기존 설치본을 먼저 삭제하지 않습니다.

```powershell
codex plugin marketplace upgrade tosun-team
codex plugin add tosun-studio@tosun-team --json
```

3. 설치 응답의 경로와 버전을 확인하고, 그 경로의 변경된 `SKILL.md` 파일을 배포 소스와 SHA-256으로 비교합니다. 저장소 푸시만으로 설치본 업데이트를 완료 처리하지 않습니다.
4. 이미 열린 대화에 새 스킬이 자동으로 다시 로드됐다고 단정하지 않습니다. 다음 새 대화에서 설치된 마스터·해당 단계 스킬을 읽어 적용합니다. 현재 대화에서 계속 작업하면 갱신된 파일을 다시 읽고 실제 사용 경로와 버전을 기록합니다.

마켓플레이스 갱신은 [OpenAI 공식 플러그인 문서](https://developers.openai.com/plugins/build/plugins)를 기준으로 합니다. 설치 파일 확인과 새 대화에서의 로드 확인은 구분하여 보고합니다.

## 비밀값

개인 지침, Higgsfield 인증 정보, API 키, 작업 결과물은 저장소에 커밋하지 않습니다.
