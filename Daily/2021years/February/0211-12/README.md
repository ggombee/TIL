### 깃 커밋 메시지 날짜 변경 방법

마지막 Commit 날짜를 현재 날짜로 설정

git commit --amend --no-edit --date "$(date)"

마지막 Commit 날짜를 임의의 날짜로 설정

git commit --amend --no-edit --date "Mon 20 Aug 2018 20:19:19 KST"

"" 사이에 원하는 날짜와 연도 및 시간을 기입하면 된다.

