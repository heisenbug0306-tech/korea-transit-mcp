# Korea Transit MCP

서울 대중교통 실시간 정보를 AI와 대화하며 조회하는 MCP 서버입니다.

[![MCP](https://img.shields.io/badge/MCP-Compatible-blue)](https://modelcontextprotocol.io)
[![Deploy](https://img.shields.io/badge/Vercel-Deployed-brightgreen)](https://koreatransitmcp.vercel.app)
[![PlayMCP](https://img.shields.io/badge/PlayMCP-Available-yellow)](https://playmcp.kakao.com)

## 왜 Korea Transit MCP인가요?

**"강남역 지하철 언제 와?"** 라고 물으면 바로 답해드립니다.

- 지하철, 버스, 따릉이 정보를 **하나의 대화**로 조회
- 복잡한 앱 전환 없이 **AI에게 물어보기만** 하면 끝
- 서울시 공공데이터 기반 **실시간 정보** 제공

---

## 제공 기능

### 6개 도구로 서울 대중교통 완벽 커버

| 도구 | 기능 | 사용 예시 |
|------|------|----------|
| `transit_get_subway_arrival` | 지하철 실시간 도착정보 | "강남역 지하철 도착정보" |
| `transit_get_subway_status` | 호선별 운행상태 | "2호선 지금 정상 운행해?" |
| `transit_get_bus_arrival` | 버스 도착정보 | "22341 정류장 버스 언제 와?" |
| `transit_search_bus_station` | 버스정류장 검색 | "서울역 근처 버스정류장 찾아줘" |
| `transit_get_bike_station` | 따릉이 대여소 현황 | "여의도 따릉이 몇 대 있어?" |
| `transit_get_combined_info` | 통합 교통정보 | "홍대입구 주변 교통정보 전부" |

---

## 사용 예시

### 지하철 도착정보

**질문**: "강남역 지하철 언제 와?"

**응답**:
```
🚇 강남역 실시간 도착정보

1. 2호선 - 성수행
   - 도착: 3분 후 (삼성 출발)
   - 방향: ⬇️ 하행

2. 신분당선 - 신사행
   - 도착: 전역 도착
   - 방향: ⬆️ 상행
```

### 버스정류장 검색 → 도착정보 조회

**질문**: "서울역 버스정류장 찾아줘"

**응답**:
```
🔍 버스 정류장 검색: "서울역"

1. 서울역버스환승센터
   - 정류장 번호: 01015

2. 서울역사박물관.경희궁앞
   - 정류장 번호: 01007
```

**이어서**: "01015 정류장 버스 도착정보"

**응답**:
```
🚌 서울역버스환승센터 버스 도착정보

1. 501번 (간선)
   - 첫번째 버스: 3분후 [2번째 전]
   - 두번째 버스: 12분후 [7번째 전]

2. 150번 (간선)
   - 첫번째 버스: 곧 도착
   - 두번째 버스: 8분후 [5번째 전]
```

### 따릉이 대여소

**질문**: "여의도 따릉이 지금 몇 대 남았어?"

**응답**:
```
🚲 따릉이 대여소 검색: "여의도"

1. 여의도역 1번출구
   - 대여 가능: 🟢 12대 / 15대 (80%)

2. 여의도공원 입구
   - 대여 가능: 🟡 4대 / 20대 (20%)
```

### 통합 교통정보

**질문**: "홍대입구 주변 교통정보 전부 알려줘"

**응답**:
```
📍 홍대입구 주변 교통정보

🚇 지하철 도착정보
- 2호선 성수행: 2분 후
- 2호선 신도림행: 5분 후
- 경의중앙선 용문행: 8분 후

🚌 버스 정류장
- 홍대입구역 (16165)
- 홍대정문 (16001)

🚲 따릉이 대여소
- 홍대입구역 2번출구: 🟢 8대 이용가능
```

---

## MCP 연결 방법

### PlayMCP (카카오)

[PlayMCP](https://playmcp.kakao.com)에서 "Korea Transit MCP" 검색 후 도구함에 추가

### Claude Desktop

`claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "korea-transit": {
      "url": "https://koreatransitmcp.vercel.app/mcp"
    }
  }
}
```

### MCP Endpoint

```
https://koreatransitmcp.vercel.app/mcp
```

---

## 데이터 출처

실시간 공공데이터를 활용합니다.

| 데이터 | 출처 | 갱신 주기 |
|--------|------|----------|
| 지하철 도착정보 | 서울 열린데이터광장 | 실시간 |
| 지하철 운행상태 | 서울 열린데이터광장 | 실시간 |
| 버스 도착정보 | 공공데이터포털 | 실시간 |
| 버스정류장 정보 | 서울 열린데이터광장 | 일 1회 |
| 따릉이 현황 | 서울 열린데이터광장 | 5분 |

---

## 지원 범위

### 지하철
- 1~9호선, 신분당선, 경의중앙선, 공항철도, 경춘선, 수인분당선, 우이신설선, 신림선

### 버스
- 서울시 전체 버스정류장 (약 11,000개)
- 간선, 지선, 마을, 광역, 공항버스

### 따릉이
- 서울시 전체 대여소 (약 2,700개)

---

## 기술 스택

- **Runtime**: Node.js + TypeScript
- **Protocol**: MCP (Model Context Protocol)
- **Deployment**: Vercel Serverless Functions
- **APIs**: 서울 열린데이터광장, 공공데이터포털

---

## 로컬 개발

```bash
# 클론
git clone https://github.com/yonghwan1106/kakao-mcp-server.git
cd kakao-mcp-server

# 설치
npm install

# 환경변수 (.env)
SEOUL_API_KEY=서울열린데이터광장_API_키
DATA_GO_KR_API_KEY=공공데이터포털_API_키

# 빌드 & 실행
npm run build
npm start
```

### API 키 발급

| API | 발급처 |
|-----|--------|
| SEOUL_API_KEY | [서울 열린데이터광장](https://data.seoul.go.kr) |
| DATA_GO_KR_API_KEY | [공공데이터포털](https://www.data.go.kr) |

---

## 라이선스

MIT

---

**Korea Transit MCP** - 서울 대중교통, AI에게 물어보세요.
