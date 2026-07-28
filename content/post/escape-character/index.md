---
title: "escape 문자처리란"
date: 2024-10-11T21:11:08+09:00
categories: ["DB"]
series: ["콩GPT"]
series_order: 14
tags: ["MySQL", "CSV", "이스케이프"]
draft: false
---

{{< series >}}

`ESCAPED BY '\\'`는 `LOAD DATA LOCAL INFILE` 명령어에서 사용되는 옵션으로, 데이터 파일 내의 특수 문자를 처리하는 방법을 지정합니다. CSV 파일을 MySQL로 가져올 때, 특수 문자나 구분 기호를 데이터 값의 일부로 포함시키기 위해 이스케이프 문자를 사용할 수 있습니다.

예를 들어, CSV 파일에 다음과 같은 데이터가 있다고 가정해봅시다.

```text
drugbank_id,sequence,left_element_id,left_element_name,right_element_id,right_element_name
DB001,1,LE001,"left, name",RE001,right_name
DB002,2,LE002,left_name,RE002,"right, name"
DB003,3,LE003,"left \"quoted\" name",RE003,"right \"quoted\" name"
```

위의 데이터에서 특수 문자인 쉼표(`,`)와 큰따옴표(`"`)가 값의 일부로 포함되어 있습니다. `LOAD DATA LOCAL INFILE` 명령어를 다음과 같이 사용하면:

```sql
LOAD DATA LOCAL INFILE "C:/Users/y_jeo/Desktop/source/Reactions.csv"
INTO TABLE reactions
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
ESCAPED BY '\\'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(`drugbank_id`, `sequence`, `left_element_id`, `left_element_name`, `right_element_id`, `right_element_name`);
```

이 경우, 데이터 파일 내에서 이스케이프 문자 `\`가 다음과 같은 역할을 합니다.

1. 쉼표(`,`)가 데이터 값의 일부로 포함될 수 있도록 합니다.
2. 큰따옴표(`"`)가 데이터 값의 일부로 포함될 수 있도록 합니다.

예시로, 데이터 파일에서 `DB003` 행의 `"left \"quoted\" name"` 부분은 `left "quoted" name`으로 해석됩니다. 이스케이프 문자 `\`가 없으면 MySQL은 큰따옴표를 필드 종료 기호로 잘못 인식할 수 있습니다.

따라서 `ESCAPED BY '\\'` 옵션은 데이터 파일 내의 특수 문자를 올바르게 처리하여 데이터가 정확하게 테이블에 삽입되도록 도와줍니다.
