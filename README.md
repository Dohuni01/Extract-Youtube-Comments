# Extract-Youtube-Comments

# YouTube 댓글 수집기 (YouTube Comment Scraper)

이 프로젝트는 **YouTube Data API v3**를 활용하여 지정된 YouTube 동영상의 **상위 댓글**을 자동으로 수집하고 JSON 파일로 저장하는 Python 스크립트입니다.  
CSV 파일에 있는 `video_id` 목록을 기반으로 각 영상의 댓글을 가져오며, **좋아요 수** 또는 **작성일** 기준으로 정렬해 상위 N개의 댓글만 추출합니다.

---

## 📌 주요 기능

- **CSV 기반 입력**: `video_id` 목록을 CSV 파일에서 읽어 처리
- **YouTube API 연동**: `googleapiclient.discovery`를 이용해 API 요청
- **댓글 필터링 및 정렬**:
  - `ORDER = relevance` → 인기순
  - `ORDER = time` → 최신순
- **좋아요 수 기준 상위 N개 추출**
- **정상/실패 결과 분리 저장**:
  - 성공 → `OUTPUT_JSON`
  - 실패 → `FAIL_JSON`
- **오류 처리**:
  - `commentsDisabled`, `quotaExceeded`, `notFound` 등의 예외 처리
---
## ⚙️ 환경 설정

### 1. Python 패키지 설치
```bash
pip install google-api-python-client pandas tqdm
```

### 2. YouTube API Key 발급
  1. Google Cloud Console 접속
  2. YouTube Data API v3 활성화
  3. API Key 생성
  4. 코드의 API_KEY 변수에 붙여넣기
---
🚀 사용 방법
1. CSV 파일 준비
video_id 컬럼을 가진 CSV 파일 생성 (예: videos_with_dates.csv)

```bash
video_id
abc123XYZ
def456UVW
```
2. 코드 실행
Jupyter Notebook에서 실행
또는 .py 파일로 변환 후 Python으로 실행
```bash
API_KEY = "발급받은 API 키"
INPUT_CSV = "/path/to/videos_with_dates.csv"
OUTPUT_JSON = "/path/to/youtube_comments.json"
FAIL_JSON = "/path/to/youtube_comment_failures.json"
TOP_N = 10
ORDER = "relevance"  # 또는 "time"
```
3. 결과 확인
  정상 수집된 댓글: `youtube_comments.json`
  실패한 요청: `youtube_comment_failures.json`
---
📜 예외 처리

`commentsDisabled` → 해당 영상에서 댓글이 비활성화된 경우

`quotaExceeded` → API 호출 한도 초과

`notFound` → 존재하지 않는 video_id

`FileNotFoundError` → CSV 경로 오류

---
📌 참고

YouTube Data API v3 문서 - https://developers.google.com/youtube/v3

`ORDER` 옵션:

    `relevance` → 인기순 정렬
  
    `time` → 최신순 정렬
  
`TOP_N `→ 영상별 상위 댓글 개수 제한
