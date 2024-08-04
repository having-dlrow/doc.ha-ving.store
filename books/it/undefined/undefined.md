# - 정규화

## 1 정규화

```
# Topic 테이블
title         | type       | description   | created    | author_id | author_name | author_profile | price | tag
--------------|------------|---------------|------------|-----------|-----------|------------------|------|------
Title1        | paper      | Tech topic    | 2022-03-01 | 1         | John Doe  | /images/johndoe.jpg | 29.99 | free, small,
Title1        | online     | Tech topic    | 2022-03-01 | 1         | John Doe  | /images/johndoe.jpg | 0 | free, small
Title2        | online     | Foo  topic    | 2022-12-01 | 2         | smith     |                     | 10000 | commercial, free
```

`쉼표`로 여러값이 들어간 경우

```
# Topic 테이블
title         | type       | description   | created    | author_id | author_name | author_profile | price
--------------|------------|---------------|------------|-----------|-----------|------------------|------
Title1        | paper      | Tech topic    | 2022-03-01 | 1         | John Doe  | /images/johndoe.jpg | 29.99
Title1        | online     | Tech topic    | 2022-03-01 | 1         | John Doe  | /images/johndoe.jpg | 0
Title2        | online     | Foo  topic    | 2022-12-01 | 2         | smith     |                     | 10000

# Topic Tag Relation테이블
topic_title    | tag_id
---------------|-------
title1         | 1
title2         | 1
title2         | 3

# Tag 테이블
id        | name
----------|-------
1         | free
3         | commercial
```

## 2 정규화

부분 함수 종속 :  'A(title)<= B(description), C(created) '

```
# Topic 테이블
title         | type       | description   | created    | author_id | author_name | author_profile | price | tag
--------------|------------|---------------|------------|-----------|-----------|------------------|------|------
Title1        | paper      | Tech topic    | 2022-03-01 | 1         | John Doe  | /images/johndoe.jpg | 29.99 | free, small,
Title1        | online     | Tech topic    | 2022-03-01 | 1         | John Doe  | /images/johndoe.jpg | 0 | free, small
Title2        | online     | Foo  topic    | 2022-12-01 | 2         | smith     |                     | 10000 | commercial, free
```

`title` 항목을 통해 테이블을 나눈다.&#x20;

<pre><code># Topic 테이블
title         | description   | created    | author_id | author_name | author_profile 
--------------|---------------|------------|-----------|-----------|------------------
Title1        | Tech topic    | 2022-03-01 | 1         | John Doe  | /images/johndoe.jpg 
Title1        | Tech topic    | 2022-03-01 | 1         | John Doe  | /images/johndoe.jpg  // 해당 Record 삭제
Title2        | Foo  topic    | 2022-12-01 | 2         | smith     |                     

<strong># Topic_Type 테이블
</strong>title         | type       | price
--------------|------------|------
Title1        | paper      | 29.99
Title1        | online     | 0 
Title2        | online     | 10000
</code></pre>

## 3 정규화

* 이행 함수 종속 :  'A(title)=> E(author\_id) <= F(author\_name)'
* 'author\_' 같은  prefix가 붙는 경우다다

```
# Topic 테이블
title         | description   | created    | author_id | author_name | author_profile 
--------------|---------------|------------|-----------|-----------|------------------
Title1        | Tech topic    | 2022-03-01 | 1         | John Doe  | /images/johndoe.jpg 
Title1        | Tech topic    | 2022-03-01 | 1         | John Doe  | /images/johndoe.jpg  // 해당 Record 삭제
Title2        | Foo  topic    | 2022-12-01 | 2         | smith     |                     

```

`author_id`을 통해 테이블을 나눈다.

```
# Topic 테이블
title         | description   | created    | author_id 
--------------|---------------|------------|-----------
Title1        | Tech topic    | 2022-03-01 | 1         
Title2        | Foo  topic    | 2022-12-01 | 2         

# Author 테이블
author_id  | author_name  | author_profile
-----------|--------------|---------------
1          | John Doe     | /images/johndoe.jpg
2          | smith        |
```

<figure><img src="../../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

## BCNF

* company(회사명) 이 author

```
# Topic 테이블
title         | description   | created    | author_id | company |
--------------|---------------|------------|-----------|----------
Title1        | Tech topic    | 2022-03-01 | 1         | A
Title1        | Tech topic    | 2022-03-01 | 1         | A
Title2        | Foo  topic    | 2022-12-01 | 2         | B

```

`author_id`을 통해 테이블을 나눈다.

```
# Topic 테이블
title         | description   | created    | author_id 
--------------|---------------|------------|-----------
Title1        | Tech topic    | 2022-03-01 | 1         
Title2        | Foo  topic    | 2022-12-01 | 2         

# Author 테이블
author_id  | author_name  | author_profile
-----------|--------------|---------------
1          | John Doe     | /images/johndoe.jpg
2          | smith        |
```



## 제 4 정규화



제 5 정규화
