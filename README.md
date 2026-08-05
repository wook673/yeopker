# 옆커렌탈

- `index.html` — 수수료 챗봇 (렌탈사별 수수료 검색 · 약정별 비교 · 사업자 접수)
- `product-catalog/catalog.html` — 제품 카탈로그 (내부용, 수수료 확인 버튼 포함)
- `product-catalog/catalog_customer.html` — 제품 카탈로그 (고객용)

## 갱신 절차 (로컬: `C:\Users\User\Claude\Projects\옆커렌탈`)

1. 월간 수수료표: `python update_chatbot.py "<종합수수료.xlsx>"`
2. 카탈로그 재크롤링 시: `product-catalog`에서 `crawler.py` → `build_catalog.py` → 상위 폴더에서 `link_catalog.py`
3. 이 폴더(site)에서 `git add -A && git commit && git push`
