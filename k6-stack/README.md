## InfluxDB + Grafana Composition

Grafana 공식 대시보드 [2587 (k6 Load Testing Results)](https://grafana.com/grafana/dashboards/2587-k6-load-testing-results/?utm_source=chatgpt.com) 를 기반으로,
`docker-compose up -d` 한 번으로 즉시 k6 결과 시각화 환경을 띄울 수 있도록 구성된 스택입니다.

Grafana와 InfluxDB가 자동으로 생성되며, Grafana는 InfluxDB에 자동 연결되고,
linear 스타일의 heatmap 으로 수정된 k6 대시보드가 자동 등록되어 별도의 설정 없이 바로 대시보드를 확인할 수 있습니다.

## What this provides

- InfluxDB (k6 결과 저장소)
- Grafana (InfluxDB 자동 연결)
- k6 결과 시각화 대시보드 자동 등록
- `docker-compose up -d` 한 번으로 즉시 사용 가능

## Getting Start

Clone 없이 k6-stack 디렉토리만 바로 설치(선택):

```bash
curl -L https://github.com/JiHongKim98/k6-stack-boilerplate/archive/refs/heads/main.tar.gz \
  | tar -xz --strip-components=1 "k6-stack-boilerplate-main/k6-stack"
```

InfluxDB 및 Grafana 컨테이너 생성:

```bash
cd k6-stack/

# InfluxDB 와 Grafana 컨테이너를 생성합니다.
docker-compose up -d
```

k6 실행:

```bash
# InfluxDB로 결과를 전송합니다
k6 run --out influxdb=http://localhost:8086/k6 ./path/your-scripts.js
```

Grafana 대시보드 접속:

```
# k6 테스트 결과를 확인합니다.
http://localhost:3000/dashboards
```
