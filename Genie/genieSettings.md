# Genie Space Context 설정

## Instructions

```
한국어로만 대답해줘.

질문에 대해 간결하고 두괄식으로 답변해줘.

모든 날짜에 대한 질문은 DATE(Sale_Datetime) 를 사용해서 답변해줘.

매년 분기는 1월에 시작합니다. 하나의 분기는 3개월로 1분기는 1월에서 3월, 2분기는 4월에서 6월, 3분기는 7월에서 9월, 4분기는 10월에서 12월입니다.

할인율 계산 공식은 항상 ROUND((try_divide((List_Price - Selling_Price), List_Price)) * 100, 2)을 사용해.

할인이 가장 많이 적용된 제품은 할인율이 가장 낮은 제품이야.
```

## SQL Queries

**2025년 1월 1일부터 7월 15일까지 홈쇼핑 채널 별 일일 수익을 알려주세요.**

```
SELECT
  `Home_Shopping_Channel`,
  DATE(`Sale_Datetime`) AS `Sale_Date`,
  SUM(`Selling_Price`) AS `Total_Revenue`
FROM
  `jaewoo_catalog`.`demo_schema`.`sales_transactions_v2`
WHERE
  DATE(`Sale_Datetime`) BETWEEN '2025-01-01' AND '2025-07-15'
GROUP BY
  `Home_Shopping_Channel`,
  `Sale_Date`
ORDER BY
  `Home_Shopping_Channel`,
  `Sale_Date`

```

## Sample Questions

* 데이터 셋에 대해서 설명해주세요.
* 2025년 1월 1일부터 7월 15일까지 홈쇼핑 채널 별 일일 수익을 알려주세요.
* 홈쇼핑 채널의 판매금액 트랜드를 표시해줘.
* 홈쇼핑 채널별 제품 그룹 별 환불 신청 비율은 어떻게 되나요?
* 가전 제품 중에 서울 지역에서 가장 잘 팔리는 제품의 비율을 그래프로 그려줘.

## Benchmark

## 홈쇼핑 데이터 분석 요청 요약

| No. | 질문 내용                                                                  |
| --- | -------------------------------------------------------------------------- |
| 1   | 2025년 1월 1일부터 7월 15일까지 홈쇼핑 채널 별 일일 수익을 알려주세요.     |
| 2   | 가전 제품 중에 서울 지역에서 가장 잘 팔리는 제품의 비율을 그래프로 그려줘. |
| 3   | 홈쇼핑 채널 별 고객이 환불 신청 건수를 일일 집계해서 정리해줘.             |
| 4   | 홈쇼핑 채널의 판매금액 트렌드를 표시해줘.                                  |
| 5   | 여성 블라우스를 가장 많이 산 고객의 연령대를 알려줘.                       |
| 6   | 2025년 1월 1일부터 7월 15일까지 홈쇼핑 채널 별 일일 수익을 알려주세요.     |


```sql

-- 5번 질문 SQL Answer
SELECT
  CASE
    WHEN YEAR(CURRENT_DATE) - YEAR(`Join_Date`) < 20 THEN '10대'
    WHEN YEAR(CURRENT_DATE) - YEAR(`Join_Date`) < 30 THEN '20대'
    WHEN YEAR(CURRENT_DATE) - YEAR(`Join_Date`) < 40 THEN '30대'
    WHEN YEAR(CURRENT_DATE) - YEAR(`Join_Date`) < 50 THEN '40대'
    ELSE '50대 이상'
  END AS `Age_Group`
FROM
  `jaewoo_catalog`.`demo_schema`.`customer_master_v2`
WHERE
  `Customer_Name` = (
    SELECT
      `Customer_Name`
    FROM
      (
        SELECT
          `Customer_Name`,
          COUNT(*) AS `Purchase_Count`
        FROM
          `users`.`hongguen_park`.`sales_transactions_v2`
        WHERE
          `Product_Name` = '여성 블라우스'
        GROUP BY
          `Customer_Name`
        ORDER BY
          `Purchase_Count` DESC
        LIMIT 1
      )
  )
```

```sql
-- 6번 질문 SQL Answer
SELECT
  `Home_Shopping_Channel`,
  DATE(`Sale_Datetime`) AS `Sale_Date`,
  SUM(`Selling_Price`) AS `Total_Revenue`
FROM
  `jaewoo_catalog`.`demo_schema`.`sales_transactions_v2`
WHERE
  DATE(`Sale_Datetime`) BETWEEN '2025-01-01' AND '2025-07-15'
GROUP BY
  `Home_Shopping_Channel`,
  `Sale_Date`
ORDER BY
  `Home_Shopping_Channel`,
  `Sale_Date`
```
