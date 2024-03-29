# Dirty Checking

JPA에서는 트랜잭션이 끝나는 시점에 변화가 있는 모든 엔티티 객체를 데이터베이스에 자동으로 반영해준다. 이때 변화가 있다는 기준은 **최초 조회 상태**이다.

  JPA에서는 엔티티를 조회하면 해당 엔티티의 조회 상태 그대로 스냅샷을 만들어놓는다.
그리고 트랜잭션이 끝나는 시점에 이 스냅샷과 비교하여 다른점이 있다면 Update Query를 데이터베이스로 전달한다. 

  당연히 이러한 상태 변경 검사의 대상은 **영속성 컨텍스트가 관리하는 엔티티**에만 적용된다.

---

- detach된 엔티티
- DB에 반영되기 전 처음 생성된 엔티티

등은 Dirty Checking 대상에 포함되지 않는다. 즉, 값을 변경해도 데이터베이스에 반영되지 않는다.

### 변경 부분만 update하고 싶을 땐?

 Dirty Checking으로 생성되는 update쿼리는 기본적으로 모든 필드를 업데이트 한다. 

<전체 필드를 업데이트하는 방식의 장점>

- 생성되는 쿼리가 같아 부트 실행시점에 미리 만들어서 재사용 가능하다.
- 데이터베이스 입장에서 쿼리 재사용이 가능하다.
- 동일한 쿼리를 받으면 이전에 파싱된 쿼리를 재사용한다.

`@Dynamic Update`로 변경 필드만 반영되도록 할 수 있다.
