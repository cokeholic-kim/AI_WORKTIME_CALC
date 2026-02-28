# FTP 자동 배포 설정 (GitHub Actions)

이 프로젝트는 `main` 브랜치에 머지되면 FTP로 서버 파일을 자동 갱신하도록 설정되어 있습니다.

## 1) 워크플로 파일
- `.github/workflows/deploy-ftp.yml`

트리거:
- `main` 브랜치 push (PR 머지 포함)
- 수동 실행(`workflow_dispatch`)

## 2) GitHub Secrets 설정
레포지토리 Settings → Secrets and variables → Actions → New repository secret

필수:
- `FTP_SERVER` : FTP 호스트 (예: `112.175.185.144`)
- `FTP_USERNAME` : FTP 계정 (예: `corona456`)
- `FTP_PASSWORD` : FTP 비밀번호
- `FTP_SERVER_DIR` : 업로드 경로 (예: `/html/`)

선택:
- `FTP_PORT` : 기본 21

## 3) 배포 범위
현재 설정은 프로젝트 루트 기준 업로드하며, 아래는 제외됩니다.
- `.github/**`
- `README.md`
- `node_modules/**`
- 기타 git 메타파일

현재 프로젝트 구조상 `index.html` 중심 배포에 맞춰져 있습니다.

## 4) 검증 방법
1. `main`에 커밋 머지
2. Actions 탭에서 `Deploy to FTP (main)` 실행 성공 확인
3. 서버 `html/index.html` 변경 반영 확인

## 5) 향후 SSH 전환
서버에 SSH가 열리면 다음으로 전환 권장:
- SSH 키 기반 배포
- rsync 기반 증분 배포
- 롤백/백업 자동화

필요 시 `deploy-ssh.yml`로 교체해서 운영하면 됩니다.
