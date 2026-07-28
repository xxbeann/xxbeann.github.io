---
title: "arch_prctl 시스템 콜에 대하여"
date: 2024-03-27T15:21:17+09:00
categories: ["운영체제"]
series: ["콩GPT"]
series_order: 3
tags: ["운영체제", "시스템 콜", "리눅스"]
draft: false
---

{{< series >}}

`arch_prctl` = **arch**itecture **p**rocess **c**ont**r**o**l**

- 하위 기능 중 하나로 `ARCH_SET_FS`가 있으며, FS 레지스터의 64비트 기본을 `addr`로 설정한다.

예시:

```text
4004  23:12:34.695470  arch_prctl(ARCH_SET_FS, 0x7f5561e94740) = 0 <0.000003>
```
