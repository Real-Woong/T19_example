# 삼겹살 사줘 — 프로토콜별 AI 결제 시연

`index.html`을 브라우저에서 엽니다. 설치·인터넷·계정이 필요 없습니다. Space 또는 →로 진행하고, ←로 되돌립니다. R은 처음부터입니다. Visa/Mastercard 선택을 바꾸면 처음부터 시작합니다.

**미래 상황을 가정한 오프라인 모의 시연입니다. 실제 쿠팡 연동·서명·토큰 발급·체인 거래·카드 승인·주문은 발생하지 않습니다.** 상품, 가격, 배송일, 가격비교 API는 모두 가상입니다.

## 60–90초 발표 대본

1. **요청** — “내일 쓸 삼겹살을 사 달라고 합니다. 상품은 3만 원, 별도 가격비교 API는 0.01 USDC까지 미리 허락했습니다.”
2. **ACP** — “AI가 후보를 찾으면 판매처와 주문 정보를 주고받습니다. 재고, 내일 배송, 총금액 21,900원을 확인합니다.”
3. **AP2** — “이 사람이 이 상품을 이 금액에 사도록 허락했는지 확인할 근거입니다. 조건을 벗어나면 다시 물어봅니다.”
4. **x402 요청** — “별도 유료 가격비교 API를 호출했더니 402 응답과 함께 조회료 0.01 USDC를 요청합니다.”
5. **x402 완료** — “미리 허락한 지갑으로 지불하면 결과를 받습니다. 이건 API 사용료입니다. 삼겹살 대금은 아직 별도입니다.”
6. **카드 승인** — “상품 대금은 판매처와 결제대행사를 거쳐 선택한 Visa 또는 Mastercard 망으로 요청하고, 카드 발급사가 승인합니다.”
7. **주문 결과** — “판매처가 주문을 확정합니다. 상품 주문·카드 승인과 API 결제 내역을 각각 받습니다.”

마무리: **“ACP는 주문, AP2는 구매 권한, x402는 이 예시의 API 비용, 카드망은 상품 대금의 결제를 맡습니다.”**

## 구성의 정확한 의미

- ACP → AP2 → x402 → 카드망은 이 시나리오의 설명 순서입니다. 하나의 표준 직렬 결제망이 아닙니다.
- ACP와 AP2를 예시 어댑터로 연결한다고 가정했습니다. 쿠팡이 이 구성을 지원한다고 주장하지 않습니다.
- AP2는 결제 수단에 독립적입니다. 화면은 서명된 권한과 주문의 일치를 설명하며 유효한 자격증명이나 서명을 생성하지 않습니다.
- x402는 별도 서비스 비용에 적용했습니다. 카드망으로 이어지는 필수 중간 단계가 아니며, API를 쓰지 않으면 이 지출도 없습니다.
- x402의 HTTP 402는 결제 요구입니다. ACP의 결제 실패 402를 x402 지원이라고 해석하지 않습니다.
- API 결제는 Base의 USDC를 쓰는 예시입니다. 요청 → 결제 요구 → 결제 데이터 포함 재요청 → 검증·정산 → 결과 수신을 표현합니다.
- 상품이 바뀌면 주문 조건과 권한을 재확인합니다. 이 시연에서는 가격비교 후 같은 상품을 유지합니다.
- Visa와 Mastercard 중 하나를 사용합니다. 카드 승인은 매입·정산 완료와 구분합니다.
- 30,000원 상품 한도에서 21,900원을 쓰면 잔여 한도는 8,100원입니다. 별도 지갑은 0.02 USDC에서 0.01 USDC가 남습니다. 두 통화의 합산이나 환산은 하지 않습니다.

## 공식 근거

- [ACP 구조](https://www.agenticcommerce.dev/docs/concepts/architecture) 및 [체크아웃](https://www.agenticcommerce.dev/docs/reference/checkout)
- [AP2 FAQ](https://ap2-protocol.org/faq/)
- [x402 결제 흐름](https://docs.cdp.coinbase.com/x402/how-it-works)
- [Visa Intelligent Commerce](https://developer.visa.com/capabilities/visa-intelligent-commerce/overview)
- [Mastercard Agent Pay](https://www.mastercard.com/global/en/news-and-trends/press/2025/april/mastercard-unveils-agent-pay-pioneering-agentic-payments-technology-to-power-commerce-in-the-age-of-ai.html)
# T19_example
