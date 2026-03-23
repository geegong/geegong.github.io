---
title: "Longest Common Subsequence"
date: 2026-01-04
categories:
  - DSA
tags:
  - Algorithms
---

## LCS (Longest Common Subsequence)

### 문제
https://leetcode.com/problems/longest-common-subsequence

### 문제 이해
주어진 텍스트들을 비교하여 공통인 글자들을 나열하여 가장 길게 만들 수 있는 문자열의 길이를 찾아낸다.
<br>
아래와 같이 abcde, gfbacfd 라는 문자열이 있는 경우 공통인 글자를 모아 만들 수 있는 가장 긴 문자열은 **bcd** 가 된다.
```text
a**bcd**e
gf**b**a**c**f**d**
=> bcd
```

### 풀이법
가장 효율적으로 풀 수 있는 방법은 DP이다.  
코드를 보면 직관적이지 않으나 아래 그림들을 보고 코드를 보면 이해하기가 훨씬 수월하다.
<br>
(하단 그림 첨부 필요)

