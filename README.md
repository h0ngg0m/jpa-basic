# JPA
## 영속성 컨텍스트
- 엔티티를 영구 저장하는 환경
- EntityManager.persist(entity)
- 영속성 컨텍스트는 논리적인 개념
- 엔티티 매니저를 통해 영속성 컨텍스트에 접근

## 엔티티 생명주기
- 비영속 (new/transient): 영속성 컨텍스트와 전혀 관계가 없는 새로운 상태
- 영속 (managed): 영속성 컨텍스트에 관리되는 상태
- 준영속 (detached): 영속성 컨텍스트에 저장되었다가 분리된 상태
- 삭제 (removed): 삭제된 상태

### 엔티티 생명주기 - 영속
```java
EntityManager em = emf.createEntityManager();
em.persist(member); // 영속
```
객체를 생성한 후 persist를 호출하면 영속성 컨텍스트에 저장된다. 트랜잭션을 커밋하면 DB에 반영된다.

### 엔티티 생명주기 - 준영속
```java
em.detach(member); // 준영속
```
영속성 컨텍스트에서 분리된 상태이다. 영속성 컨텍스트가 제공하는 기능을 사용할 수 없다.

### 엔티티 생명주기 - 삭제
```java
em.remove(member); // 삭제
```
삭제된 상태이다. 트랜잭션을 커밋하면 DB에서 삭제된다.

## 영속성 컨텍스트의 이점
- 1차 캐시: 조회한 엔티티를 1차 캐시에 저장하여 재사용, 동일한 트랜잭션 내에서만 유효하기 때문에 그렇게까지 큰 이점은 없다.
- 동일성 보장: 1차 캐시로 반복 가능한 읽기(REPEATABLE READ) 등급의 트랜잭션 격리 수준을 데이터베이스가 아닌 애플리케이션 차원에서 제공
- 트랜잭션을 지원하는 쓰기 지연
<img width="953" alt="Screenshot 2024-05-22 at 2 19 37 PM" src="https://github.com/h0ngg0m/jpa-basic/assets/125632083/2c7794db-f5af-405c-8875-f109825ab73e">

- 변경 감지(Dirty Checking)
- 지연 로딩(Lazy Loading)
