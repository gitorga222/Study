# Spring boot Page 나누기

📖 page를 나누기 위해 repository에 새로운 함수를 만듬.

### 1️⃣ Page 객체 만들기
```
Page<Party> findPageBy(Pageable page);
```
- Page를 나누기 위한 객체

### 2️⃣ Repository에 함수 만들기
```
@Query(value = "select * from party where match(Starting_point) against(?1)", nativeQuery = true)
List<Party> getPartyById(String text);
```
- `@Query` 문으로 함수의 행동에 대한 쿼리문을 만들어줌.

### 3️⃣ Service 만들기
```
public Page<Party> getPartyList(Integer i) {
    Page<Party> partyList = partyRepository.findPageBy(PageRequest.of(i, 20));
    return partyList;
}
```
- PageRequest.of(i, 20) `i는 현재 페이지인지 20은 페이지마다 띄울 총 개수`
### 4️⃣ Controller 만들기

```
@GetMapping("/party/list/{i}")
public void listParty(@PathVariable Integer i) {
    partyService.getPartyList(i);
}
```
`{i}`를 `@RathVariable`로 받아서 Service에 `파라미터`로 넘겨준다.