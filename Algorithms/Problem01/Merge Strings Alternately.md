# Problem 01 - Merge Strings Alternately

## 문제 설명
두 개의 문자열 `word1`과 `word2`가 주어집니다.  
문자열을 번갈아가며 문자를 추가하는 방식으로 병합한 문자열을 반환하세요.  
`word1`부터 시작하며, 한 쪽 문자열이 더 길 경우 남은 문자는 병합 문자열 뒤에 그대로 붙입니다.

---

## 접근 방식

### Approach 1: Two Pointers

**직관**  
두 포인터 `i`, `j`를 각각 `word1`, `word2`의 시작점에 두고, 번갈아가며 문자를 `result`에 추가합니다.

**알고리즘**
1. 두 문자열의 길이 `m`, `n`을 구합니다.
2. `i`, `j`는 0부터 시작합니다.
3. `i < m`인 동안 `word1[i]`를 추가하고, `i`를 증가.
4. `j < n`인 동안 `word2[j]`를 추가하고, `j`를 증가.
5. 두 문자열을 모두 다 순회할 때까지 반복합니다.

**파이썬 구현 요령**
- 문자열은 불변(immutable)이라 `list`에 문자를 추가하고, 마지막에 `"".join(result)`로 병합합니다.

```python
class Solution(object):
    def mergeAlternately(self, word1, word2):
        m = len(word1)
        n = len(word2)
        i = 0
        j = 0
        result = []

        while i < m or j < n:
            if i < m:
                result += word1[i]
                i += 1
            if j < n:
                result += word2[j]
                j += 1

        return "".join(result)
```

### Approach 2: One Pointer

**직관**  
단일 포인터 `i`를 사용하여 `max(len(word1), len(word2))`만큼 순회하며 두 문자열에서 각 인덱스의 문자가 존재하면 병합 문자열에 추가합니다.

**알고리즘**
1. `i`를 0부터 시작하여 `max(m, n)`까지 반복.
2. `i < m`이면 `word1[i]` 추가.
3. `i < n`이면 `word2[i]` 추가.

---

## 테스트 케이스

| word1  | word2  | 출력 결과 | 설명                         |
|--------|--------|-----------|------------------------------|
| "abc"  | "pqr"  | "apbqcr"  | 번갈아가며 모두 병합됨      |
| "ab"   | "pqrs" | "apbqrs"  | word2의 나머지가 뒤에 붙음   |
| "abcd" | "pq"   | "apbqcd"  | word1의 나머지가 뒤에 붙음   |

---

## 시간 복잡도 & 공간 복잡도

- 시간 복잡도: `O(m + n)`  
  두 문자열을 순회하면서 결과 문자열을 만듭니다.

- 공간 복잡도:
  - **파이썬**: 리스트를 사용한 후 `.join()` → 총 `O(m + n)`
  - **C++**: 문자열은 가변이라 O(m+n)
  - **Java**: `StringBuilder` 사용 → O(m+n)

---
