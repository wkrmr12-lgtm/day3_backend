# day3_backend — 제주 미세먼지 FastAPI

공공데이터(에어코리아) → FastAPI 가공·예측 → Supabase 저장. 키는 서버(Railway Variables)에만 둡니다.

## 로컬 실행
```bash
python3 -m venv vjeju
./vjeju/bin/pip install --only-binary=cryptography -r requirements.txt
cp .env.example .env   # 값 채우기
./vjeju/bin/uvicorn main:app --reload --port 8000
```
확인: http://127.0.0.1:8000/health , /docs

## Railway 배포
1. New Project → Deploy from GitHub repo → 이 저장소 선택
2. Variables → Raw Editor 에 입력
```
SUPABASE_URL=https://xxxx.supabase.co
SUPABASE_SECRET_KEY=sb_secret_...
DATA_GO_KR_KEY=
ADMIN_TOKEN=직접정한긴문자열
SIDO_NAME=제주
COLLECT_MINUTES=60
FRONT_ORIGINS=https://내-vercel-주소.vercel.app
```
3. Deploy → Active(초록) 확인
4. Settings → Networking → Generate Domain → `<주소>/health` 확인
5. Serverless(App Sleeping)는 끈다 (자동 수집 유지)

## Supabase
SQL Editor 에서 `schema.sql` 실행 (air_readings, collect_logs).
