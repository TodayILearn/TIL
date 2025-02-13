# 📌 TIL: Primary Key와 ID 중복 검사  

## 1️⃣ **문제점: ID 중복 검사를 하면 Primary Key가 필요 없을까?**  
### ❌ 처음 생각  
- `user_id`가 중복되지 않도록 하면, `id`(PK) 없이도 회원을 관리할 수 있지 않을까?  
- `user_id`를 PK로 사용하면, 별도의 `id` 컬럼 없이도 회원을 식별할 수 있지 않을까?  

### ⚠️ **하지만, 문제 발생!**  
1. **PK는 내부적으로 관리되는 식별자 역할을 해야 함.**
   - `user_id`는 사용자가 직접 입력하는 값이므로, PK로 쓰기에는 위험할 수 있음.  
   - **보안 및 개인정보 보호 이슈** 발생 가능.  
   
2. **PK는 짧고 최적화된 값이 유리함.**
   - `user_id`는 보통 **문자열(VARCHAR)** 형태인데, PK로 쓰면 **검색 속도가 느려짐.**  
   - DB에서 **숫자형 PK가 성능 최적화에 유리**함.  

3. **외래 키(FK)로 사용할 때 성능 저하**
   - 다른 테이블에서 `user_id`를 **외래 키(FK)** 로 사용하면,  
     - 문자열 기반 인덱스가 생성되므로 **JOIN 성능이 저하**됨.  
     - **숫자 기반 PK**가 더 효율적임.  

---

## 2️⃣ **해결법: `id (PK)` + `user_id (UNIQUE)` 조합 사용!**  
### ✅ **최적의 테이블 구조 (MySQL 예제)**  
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,          -- 내부적으로 관리되는 ID
    user_id VARCHAR(50) UNIQUE NOT NULL,  -- 사용자 ID (변경 불가)
    password TEXT NOT NULL
);
```
### ✅ PK + UNIQUE 조합 예제 (Supabase, JavaScript)
``` javascript

await supabase
  .from("users")
  .insert([{ id: crypto.randomUUID(), user_id: "test123", password: "hashed_pw" }]);
```

✔ PK는 숫자형 (자동 증가 or UUID)로 유지
✔ user_id는 UNIQUE + 변경 불가로 설정
✔ 데이터 조회 및 관계형 DB 최적화 🚀

## 3️⃣ 느낀 점
✔ PK는 내부적으로 빠른 조회를 위해 사용되므로, 숫자형 ID가 더 적합하다.
✔ user_id를 변경 불가능하게 하더라도, FK 관계 및 성능 문제로 인해 PK로 쓰는 것은 비효율적이다.
✔ 따라서 id (PK) + user_id (UNIQUE) 조합이 가장 확장성과 성능이 좋은 구조이다.
✔ 앞으로 DB 설계를 할 때, PK와 UNIQUE 키의 역할을 명확하게 구분해야겠다.