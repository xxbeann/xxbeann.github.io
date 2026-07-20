---
title: "N+1 문제와 fetch join"
description: "지연 로딩과 N+1, 그리고 해결법"
date: 2026-03-20T09:00:00+09:00
categories: ["Spring"]
tags: ["JPA", "성능"]
series: ["JPA 정복기"]
series_order: 2
---

{{< series >}}

N+1은 연관 엔티티를 지연 로딩할 때, 조회한 엔티티 수(N)만큼 추가 쿼리가 나가는 문제다.

## 해결책

- **`fetch join`** (JPQL) — inner join으로 한 번에
- **`@EntityGraph`** — left join으로 한 번에 ([이전 글](/jpa-entitygraph-left-join/) 참고)
- **`@BatchSize` / `default_batch_fetch_size`** — IN 절로 묶어 N번 → 1번

> 컬렉션 페치 조인 + 페이징을 같이 쓰면 `HHH000104` 경고와 함께 메모리에서 페이징되니 주의.
