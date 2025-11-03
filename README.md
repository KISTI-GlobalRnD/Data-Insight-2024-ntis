# 데이터 인사이트 및 혁신전략 분석 – GitHub 시범 페이지

## 보고서 · 링크 · 문의
- GitHub Pages: https://kisti-globalrnd.github.io/Data-Insight-2024-ntis/
- 보고서 소개: [KISTI 데이터 인사이트](https://www.kisti.re.kr/post/data-insight?t=1744699800073)
- GitHub 조직: [Global R&D GitHub](https://github.com/KISTI-GlobalRnD)
- 프로젝트 개요: [Global R&D 소개 페이지](https://dap.kisti.re.kr/globalrnd)
- 연구 책임자: [김영진 선임 연구원 LinkedIn](https://www.linkedin.com/in/young-jin-kim-8606b9142/)
- 문의: 김영진 선임 연구원 <kimyoungjin06@kisti.re.kr>

## 개요
- 본 디렉터리는 「데이터 인사이트 및 혁신전략분석보고서」의 공개·재현성 강화를 위한 GitHub 자매 페이지(시범) 자료를 제공합니다.
- `make_Web.ipynb` 노트북을 기반으로 Plotly 인터랙티브 시각화를 생성하고, 분석에 사용된 데이터셋과 산출물을 함께 제공합니다.
- 공개 데이터는 최종 분석이 완료된 범위 내에서 개인정보 및 민감 정보가 제거된 공개 가능 버전만 포함합니다.
- HTML 자산(`index.html`, `scatter_th*.html`)은 GitHub Pages에 업로드하면 바로 임베드할 수 있도록 구성되어 있습니다.

## 공개 자료 구조
- `index.html` : 임계값(Threshold) 선택 버튼과 iframe으로 구성된 대시보드 메인 페이지.
- `scatter_th{1,10,50,100}.html` : Plotly로 생성된 인터랙티브 산점도. `P10` 지표에 대한 최소값 필터를 각각 적용했습니다.
- `Data/` : 분석 재현을 위해 공개한 Parquet 포맷 데이터.
- `make_Web.ipynb` : 위 HTML 파일을 생성하는 Jupyter Notebook. Python 3.10+ 환경에서 실행 가능합니다.

## 데이터 설명 (`Data/`)
| 파일명 | 설명 | 주요 컬럼 |
| --- | --- | --- |
| `dashboard_data.parquet` | 사업명·과제유형 단위로 집계한 성과지표 요약 데이터. Plotly 산점도의 기본 데이터소스로 사용됩니다. | `P1`, `PP1`, `PR1`, `PF1`, `P5`, `PP5`, `PR5`, `PF5`, `P10`, `PP10`, `PR10`, `PF10`, 각 `*_frac` 비율 값, `과제유형`, `Total Fund` 등 |
| `dashboard_data_sub.parquet` | 과제유형별 논문/특허 건수 요약본. 산점도에서 하이브리드/단일 유형을 구분하는 보조 지표로 활용합니다. | `자유공모형`, `하향식`, `품목지정형` 등 유형별 건수 |

> 지표 기호(P, PP, PR, PF 등)의 상세 정의는 본 보고서 본문을 참조해 주십시오.

## 재현 방법
1. Python 환경 준비  
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   pip install pandas plotly tqdm matplotlib
   ```
2. 노트북 실행  
   - `make_Web.ipynb`을 열어 셀을 위에서부터 순차 실행합니다.  
   - 필요 시 `Data/` 경로를 환경에 맞게 조정합니다.
3. HTML 산출물 확인  
   - 실행이 완료되면 `scatter_th*.html`이 생성됩니다.  
   - `index.html`의 버튼은 동일 디렉터리 내의 HTML 파일을 참조하므로, 폴더 전체를 GitHub Pages에 업로드하면 즉시 활용할 수 있습니다.

## 활용 및 참고
- `index.html`은 Tailwind 기반의 간단한 레이아웃으로 작성되어 있어 추가 섹션(예: 텍스트 설명, 추가 링크)을 손쉽게 확장할 수 있습니다.
- 다른 임계값 또는 축 조합을 시험하려면 노트북 내 `axis_options`, `threshold` 리스트를 수정 후 다시 실행하면 됩니다.
- 추가적인 시각화나 데이터 파생 작업을 수행할 경우, 원본 데이터(`Data/*.parquet`)를 참고해 분석 컨텍스트를 유지해 주세요.
