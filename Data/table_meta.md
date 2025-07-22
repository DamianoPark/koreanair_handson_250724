# 📄 테이블 메타 정보

## 📁 customer_master_v2

| 컬럼명           | 데이터 타입 | 설명 |
|------------------|-------------|------|
| Customer_Name    | string      | 고객 이름 |
| Join_Date        | date        | 고객 가입 일자 |
| Membership_Grade | string      | 고객 멤버십 등급. 현재 사용되는 값은 "Gold","VIP","Silver". |
| Region           | string      | 고객 거주 지역 |

**AI Suggested Description:**  
The table contains information about customers, including their names, join dates, membership grades, and regions. This data can be used for analyzing customer demographics, tracking membership trends, and understanding regional distribution of customers. Possible use cases include targeted marketing strategies and evaluating the effectiveness of membership programs.

---

## 📁 sales_transactions_v2

| 컬럼명              | 데이터 타입 | 설명 |
|---------------------|-------------|------|
| Customer_Name       | string      | 고객 이름 |
| Sale_ID             | string      | 각 판매 거래의 고유 식별자 |
| Sale_Datetime       | timestamp   | 판매 거래가 발생한 날짜 및 시간을 나타내는 타임스탬프 |
| Product_Name        | string      | 판매되는 제품명 |
| Product_Group       | string      | 제품 그룹으로 제품에 대한 대분류. 현재 사용되는 값은 "뷰티", "리빙", "가전", "패션". |
| Product_Category    | string      | 제품 카테고리로, 제품에 대한 소분류. 현재 사용되는 값은 "주방가전", "무선청소기", "남성의류", "스킨케어", "주방용품", "신발", "가구", "전자기기", "여성의류", "침구류", "헤어케어", "메이크업". |
| Selling_Price       | bigint      | 할인율이 적용된 제품 판매가 |
| List_Price          | bigint      | 할인율이 적용되지 않은 제품 원가 |
| Currency            | string      | 제품 판매가 및 제품 원가의 기준 통화. 현재 사용되는 값은 "KRW" 로 한국 통화. |
| Home_Shopping_Channel | string    | 거래가 발생한 홈쇼핑 채널명. 현재 사용되는 값은 "롯데홈쇼핑","현대홈쇼핑","신세계라이브쇼핑","CJ오쇼핑","GS샵". |
| Order_Method        | string      | 주문 방법. 현재 사용되는 값은 "Mobile","Web","Phone". |
| Refund_Status       | string      | 환불 신청 여부. 현재 사용되는 값은 "Y","N". |

**AI Suggested Description:**  
The table contains sales transaction data for products sold through home shopping channels. It includes details such as customer names, unique sale identifiers, timestamps of sales, product information, pricing, and order methods. This data can be used to analyze sales trends, customer purchasing behavior, and the performance of different home shopping channels.
