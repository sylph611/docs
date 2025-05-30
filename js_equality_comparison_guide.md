
# 🧠 JavaScript 비교 연산자 완전 정리

이 문서는 JavaScript에서 사용하는 비교 연산자들인 `!==`, `!=`, `==`, `===`, `Object.is()`의 차이점을 정리한 가이드입니다.

---

## 1. `==` (느슨한 동등 비교, Loose Equality)

- **타입이 다르면 자동 형 변환 후 비교**
- **주의 필요**: 예상치 못한 결과를 낼 수 있음

### 예시
```js
"5" == 5           // true
0 == false         // true
null == undefined  // true
[] == false        // true
```

---

## 2. `===` (엄격한 동등 비교, Strict Equality)

- **형 변환 없이 값과 타입이 모두 같아야 true**
- 일반적으로 추천되는 방식

### 예시
```js
"5" === 5          // false
0 === false        // false
null === undefined // false
5 === 5            // true
```

---

## 3. `!=` (느슨한 부등 비교, Loose Inequality)

- `==`의 부정형
- 형 변환이 일어난 후 다르면 `true`

### 예시
```js
"5" != 5           // false
null != undefined  // false
0 != false         // false
```

---

## 4. `!==` (엄격한 부등 비교, Strict Inequality)

- `===`의 부정형
- 타입 또는 값 중 하나라도 다르면 `true`

### 예시
```js
"5" !== 5          // true
null !== undefined // true
0 !== false        // true
5 !== 5            // false
```

---

## 5. `Object.is()` (정밀 비교)

- `===`와 거의 동일하지만,
  - **`NaN === NaN` → false**, `Object.is(NaN, NaN)` → **true**
  - **`+0 === -0` → true**, `Object.is(+0, -0)` → **false**

### 예시
```js
Object.is(5, 5)           // true
Object.is("5", 5)         // false
Object.is(NaN, NaN)       // true
Object.is(+0, -0)         // false
Object.is(null, undefined)// false
```

---

## ✅ 비교 요약표

| 비교        | 형 변환 | 타입 검사 | `NaN == NaN` | `+0 == -0` | 일반 비교 추천 |
|-------------|----------|------------|---------------|--------------|-----------------|
| `==`        | ✅ 있음   | ❌ 느슨함   | ❌ false       | ✅ true       | ❌ 사용 지양     |
| `===`       | ❌ 없음   | ✅ 엄격함   | ❌ false       | ✅ true       | ✅ 표준 방식     |
| `!=`        | ✅ 있음   | ❌ 느슨함   | ✅ true        | ✅ false      | ❌ 사용 지양     |
| `!==`       | ❌ 없음   | ✅ 엄격함   | ✅ true        | ✅ false      | ✅ 안전한 비교   |
| `Object.is` | ❌ 없음   | ✅ 엄격함   | ✅ true        | ❌ false      | ☑️ 특수 용도     |

---

## 🎯 결론

- **일반적인 비교에는 `===` 와 `!==` 사용을 권장**합니다.
- **정밀한 비교 (e.g. `NaN`, `+0/-0`)가 필요한 경우에는 `Object.is()`를 사용**합니다.
- `==` 와 `!=`은 형 변환 때문에 버그 유발 가능성이 크므로 **사용 지양**하는 것이 좋습니다.
