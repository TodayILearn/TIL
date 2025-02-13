# 🚀 Authentication 없이 로그인 구현한 문제점과 해결법

## 🔍 문제점 (현재 방식의 보안 취약점)

이번에 로그인 기능을 개발하면서 Supabase를 사용했지만, **Authentication 없이 단순한 ID/PW 조회 방식**으로 구현했다.  
이 과정에서 **심각한 보안 문제**가 존재한다는 걸 깨달았다.

### ❌ 현재 방식의 문제점

1. **비밀번호 암호화 안 함**
   - 사용자가 입력한 `password`가 **그대로 DB에 저장됨**
   - 해킹 시 모든 비밀번호가 노출될 위험이 큼
2. **JWT 인증 없음**

   - 로그인 성공 후에도 인증 토큰이 없어서 **사용자의 로그인 상태 유지 불가**
   - API 호출 시 인증을 할 방법이 없음

3. **보안 취약한 로그인 검증**
   - 로그인 시 `SELECT * FROM users WHERE user_id = ? AND password = ?` 로 검증
   - **SQL Injection 공격 가능성**이 존재
   - 해커가 비밀번호를 그대로 탈취할 위험이 있음

---

## ✅ 해결법 (보안 강화)

이러한 보안 문제를 해결하기 위해 **다음과 같은 방법으로 개선해야 한다.**

### 1️⃣ **비밀번호 암호화 (bcrypt 사용)**

현재 비밀번호를 **평문(plain text)**으로 저장하는 것이 문제이므로,  
**bcrypt를 사용하여 비밀번호를 해싱(hash)**하고 저장해야 한다.

📌 **수정 방법:**

- `bcrypt` 라이브러리를 사용하여 비밀번호를 해싱한 후 DB에 저장
- 로그인 시 입력한 비밀번호를 해싱하여 DB의 해시값과 비교

```javascript
const bcrypt = require("bcrypt");

// 비밀번호 해싱 후 DB 저장
const hashedPassword = await bcrypt.hash(password, 10);

await supabase.from("users").insert([{ user_id, password: hashedPassword }]);
```

### 2️⃣ JWT 인증 추가 (jsonwebtoken)

로그인 성공 시 JWT(JSON Web Token)를 발급하여 사용자의 인증 상태를 유지해야 한다.

📌 수정 방법:

- 로그인 성공 시 JWT를 발급
- 이후 API 호출 시 JWT를 헤더에 포함하여 인증

```
javascript

const jwt = require("jsonwebtoken");

const token = jwt.sign({ user_id: user.id }, "SECRET_KEY", { expiresIn: "1h" });

// 클라이언트에 JWT 토큰 전달
res.json({ message: "로그인 성공", token });
```

### 3️⃣ Supabase Auth 사용 (더 간단한 방법)

Supabase 자체에서 제공하는 **"Supabase Auth"**를 사용하면,
직접 로그인 기능을 구현하지 않고도 안전한 인증이 가능하다.

📌 적용 방법:

- `supabase.auth.signUp()`으로 회원가입 시 비밀번호는 자동으로 암호화됨
- `supabase.auth.signInWithPassword()`로 로그인하면 토큰이 자동 발급됨

```javascript
const { data, error } = await supabase.auth.signUp({
  email: "test@example.com",
  password: "securepassword",
});
```

```javascript
const { data, error } = await supabase.auth.signInWithPassword({
  email: "test@example.com",
  password: "securepassword",
});
```

## 💡 느낀 점
로그인 기능을 단순하게 구현하면서 보안이 얼마나 중요한지 깨닫게 되었다.
비밀번호를 암호화하지 않고 저장하는 것만으로도 치명적인 보안 취약점이 될 수 있고,
JWT 같은 인증 방식을 추가하지 않으면 사용자의 로그인 상태를 유지할 방법이 없다는 것도 알게 되었다.

이번 경험을 통해,
✔ 기본적인 인증 시스템도 보안이 매우 중요하다.
✔ 무조건 비밀번호는 해싱해서 저장해야 한다.
✔ 가능하면 직접 구현하지 말고 Supabase Auth 같은 인증 서비스를 활용하는 것이 좋다.
