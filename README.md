Arknights Derivatives Exchange Simulator (ADES)

명일방주(Arknights) 세계관의 국가들을 현실 국가의 경제 데이터와 연동하여 가상의 외환시장(Forex) 및 파생금융상품을 시뮬레이션하는 프로젝트입니다.

실시간 환율 API를 이용하여 명일방주 국가 화폐의 가치를 계산하고, 선물(Futures), 옵션(Options), ETF, 국채 등의 수익률을 한국 원화(KRW) 기준으로 표시합니다.

주요 기능
실시간 환율 연동
실시간 환율 API 연동
KRW 기준 환산
국가별 환율 자동 갱신
환율 이력 저장
명일방주 국가 화폐 시스템
국가	현실 모티브	가상 통화	현실 통화
Victoria	영국	VPD	GBP
Ursus	러시아	URB	RUB
Yan	중국	YNB	CNY
Kazimierz	폴란드	KZM	PLN
Laterano	바티칸	LTR	EUR
Columbia	미국	CLD	USD
Leithanien	독일	LTH	EUR
Higashi	일본	HGS	JPY
프로젝트 목표

본 프로젝트는 다음과 같은 가상 금융 시스템을 구현하는 것을 목표로 합니다.

외환 거래소(Forex)
통화 선물(FX Futures)
통화 옵션(FX Options)
국가 ETF
국채
CDS (신용부도스왑)
오리지늄 선물
국가 위험도 지수
이동도시 산업 지수
시스템 구조
실시간 환율 API
        │
        ▼
환율 수집 모듈
        │
        ▼
명일방주 통화 변환기
        │
        ├── 외환시장
        ├── ETF
        ├── 국채
        ├── 선물
        └── 옵션
        │
        ▼
수익률 계산
        │
        ▼
KRW 환산
        │
        ▼
웹 대시보드
설치
저장소 복제
git clone https://github.com/your-id/arknights-derivatives-exchange.git

cd arknights-derivatives-exchange
패키지 설치
pip install -r requirements.txt
requirements.txt
requests
pandas
numpy
streamlit
plotly
sqlalchemy
python-dotenv
환율 API 설정

환경변수 파일 생성

.env

EXCHANGE_API_KEY=YOUR_API_KEY
예제 코드
실시간 환율 조회
import requests

def get_rate(base, target):

    url = (
        f"https://api.exchangerate.host/convert"
        f"?from={base}&to={target}"
    )

    response = requests.get(url)
    data = response.json()

    return data["result"]

print(get_rate("USD", "KRW"))
명일방주 통화 매핑
ARKNIGHTS_CURRENCIES = {

    "Victoria": {
        "symbol": "VPD",
        "real": "GBP",
        "multiplier": 1
    },

    "Ursus": {
        "symbol": "URB",
        "real": "RUB",
        "multiplier": 100
    },

    "Yan": {
        "symbol": "YNB",
        "real": "CNY",
        "multiplier": 10
    },

    "Columbia": {
        "symbol": "CLD",
        "real": "USD",
        "multiplier": 1
    }
}
선물 수익률 계산
def futures_profit(
    principal,
    entry_rate,
    current_rate
):

    profit_rate = (
        current_rate - entry_rate
    ) / entry_rate

    profit = (
        principal * profit_rate
    )

    return profit_rate, profit
출력 예시
=================================
Victoria FX Futures
=================================

투자금액
10,000,000 KRW

진입환율
1,800 KRW

현재환율
1,920 KRW

수익률
6.67%

예상수익
667,000 KRW
향후 개발 계획
Version 1.0
실시간 환율
통화 변환
선물 수익률 계산
Version 2.0
Streamlit 대시보드
환율 차트
투자 포트폴리오
Version 3.0
옵션 거래
블랙-숄즈 모델
변동성 지수(VIX)
Version 4.0
멀티플레이어 거래소
길드 금융 시스템
가상 중앙은행
기술 스택
Backend
Python
FastAPI
SQLAlchemy
PostgreSQL
Frontend
Streamlit
Plotly
Data
ExchangeRate API
Currency API
라이선스

MIT License

Disclaimer

본 프로젝트는 명일방주 세계관을 기반으로 한 팬 프로젝트입니다.

실제 투자 목적이 아닌 학습 및 시뮬레이션 용도로 제작됩니다.

Hypergryph, Studio Montagne, Yostar와는 공식적인 관련이 없습니다.
