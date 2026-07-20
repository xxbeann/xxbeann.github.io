---
title: "@EntityGraph는 결국 left join이다"
description: "EntityGraph와 JPQL join fetch의 조인 방향 차이"
date: 2026-03-10T09:00:00+09:00
categories: ["Spring"]
tags: ["JPA", "성능"]
series: ["JPA 정복기"]
series_order: 1
---

{{< series >}}

JPA에서 `@EntityGraph`와 JPQL `join fetch`는 둘 다 "페치 조인"이지만 **기본 조인 방향이 다르다.**

## 결론

| 방식 | 조인 타입 |
|------|-----------|
| `@EntityGraph` | **LEFT OUTER JOIN** |
| JPQL `join fetch` | INNER JOIN |
| JPQL `left join fetch` | LEFT OUTER JOIN |

## 왜 중요한가

`@EntityGraph`는 left join이라 **연관 데이터가 없어도(null·빈 컬렉션) 루트 엔티티가 결과에서 사라지지 않는다.**

```java
@EntityGraph(attributePaths = "team")
List<Member> findAll(); // team 없는 member도 포함됨
```

만약 `join fetch`(inner)로 했다면 team 없는 member는 결과에서 빠진다. `type`(FETCH/LOAD)은 조인 방향과 무관하며, 그래프에 넣은 속성은 언제나 left outer join으로 나간다.
