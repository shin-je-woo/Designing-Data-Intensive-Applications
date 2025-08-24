# 데이터 모델과 질의 언어

> **"실력 없는 프로그래머는 코드 작성에만 집착한다. 뛰어난 프로그래머는 데이터가 어떻게 조직되고 연결되는지에 더 신경 쓴다."**

솔직히 말해보자. 우리 모두 한 번쯤은 단지 인기 있다는 이유로 데이터베이스를 선택한 적이 있다. <br>
하지만 데이터 모델은 단순히 정보를 저장하는 공간이 아니다. 앱의 뼈대다. 잘못 설계하면 밤새워 땜질하느라 고생하게 된다.

## 🕰️ 데이터 혼돈의 역사 한눈에 보기

### 관계형 데이터베이스의 등장 (1970년대~현재)

관계형 데이터베이스는 현대 데이터 관리의 기반이 되었다. <br>
신뢰할 수 있고, 익숙하며, 널리 사용된다.

- **테이블과 행**: 스프레드시트처럼 구조화되어 있지만 훨씬 더 강력하고 유연하다.
- **SQL**: "WHERE" 같은 개념을 일상 개발에 도입한 표준 쿼리 언어.
- **일상 속 영향력**: 은행 ATM부터 데이팅 앱까지 핵심 시스템을 구동한다.

**표준이 된 이유:**

✔️ 단순하고 직관적인 데이터 구조

✔️ 데이터 무결성을 보장하는 신뢰할 수 있는 ACID 트랜잭션

✔️ 업계 전반에서 입증된 안정적인 선택지

<img width="528" height="470" alt="Image" src="https://github.com/user-attachments/assets/1301b399-e7fa-49fd-9725-270ff8c1c2bb" />

### 초기 데이터베이스 모델들

SQL과 관계형 데이터베이스가 대세가 되기 전, 다양한 데이터베이스 모델이 데이터 관리 문제를 해결하려 했다.

| 데이터베이스 모델 | 강점 | 한계 | 유산 |
| --- | --- | --- | --- |
| 계층형(IMS) | 초기 컴퓨팅에 매우 빠름 | 복잡한 관계 처리에 약함 | 문서형 DB 설계에 영향 |
| 네트워크(CODASYL) | 유연하고 풍부한 연결 지원 | 설계와 유지보수가 어려움 | 지나치게 복잡한 연결의 단점 부각 |
| 객체지향 | 객체지향 프로그래밍과 밀접 | DB 요구사항에 항상 적합하지 않음 | ORM 도구에 영감 제공 |
| XML DB | 사람이 읽을 수 있는 형식 | 대규모에서는 관리가 번거로움 | 초기 웹 서비스, 데이터 교환 포맷에 영향 |

## NoSQL 혁명: 전통적 테이블을 넘어서

2010년대에 들어, 고정된 테이블 구조의 한계가 대규모 웹앱에서 두드러지기 시작했다. 개발자들은 더 유연한 데이터 저장·조회 방식을 모색했다.

**문서형 데이터베이스 (예: MongoDB, CouchDB):**

- **유연한 구조**: 스키마가 동적으로 변해 데이터 모델이 진화 가능.
- **중첩 데이터**: JSON 같은 계층적 데이터 저장 지원.
- **단순 쿼리에 최적화된 고성능**: 문서 단위 신속 조회에 강점, 문서 간 복잡한 관계는 관리가 어려울 수 있음.

**실제 사용 예시**:

```json
{
  "startup_phase": "pre-revenue",
  "tech_stack": ["Blockchain", "AI", "NFT"],
  "burn_rate": "$100k/month",
  "exit_strategy": "Acquired by Google (please)"
}
```

이 변화로 데이터 내 일대다(one-to-many) 관계가 늘어났다. 각 JSON 문서는 다음과 같이 보인다:

<img width="464" height="335" alt="Image" src="https://github.com/user-attachments/assets/d9e8c1dd-ec80-4862-b477-adba55ef8c3c" />

## 관계형 vs. 문서형 데이터베이스, 무엇이 더 나을까?

### 문서형 데이터베이스가 적합한 경우:

- 데이터가 계층적 구조(중첩 폴더, 마트료시카 인형 등)와 유사할 때
- 고정된 스키마를 자주 바꾸지 않고 유연성을 원할 때
- 전체 레코드 또는 관련 데이터를 한 번에 조회/표시하는 게 주요 목적일 때

### 관계형 데이터베이스가 강력한 경우:

- 데이터가 복잡하게 연결되어 있을 때(모두가 연결된 소셜 네트워크 등)
- 여러 엔터티를 조합·필터하는 상세 쿼리가 필요할 때(특정 지역 거주 구매 고객 찾기 등)
- 데이터의 일관성과 무결성이 매우 중요할 때

| 시나리오 | 문서형 DB 장점 | 관계형 DB 장점              |
| --- | --- |------------------------|
| 댓글이 달린 블로그 글 | 단일 문서 모델로 단순 | 여러 테이블과 조인 필요          |
| 은행 시스템 | 일관성 보장 어려움 | 원자적이고 신뢰할 수 있는 트랜잭션 지원 |
| 소셜 네트워크 | 복잡한 관계 모델링 어려움 | 그래프처럼 복잡한 join 쿼리에 강점  |

이것이 바로 다대다(many-to-many) 관계 관리에 있어 관계형 데이터베이스가 선호되는 주요 이유 중 하나다.

<img width="741" height="502" alt="Image" src="https://github.com/user-attachments/assets/b3bbf8a9-b661-4875-b8be-ce65ca3e453e" />

## 혼합 접근: 두 데이터베이스 스타일의 장점 결합

최신 데이터베이스는 관계형과 문서형 모델의 강점을 결합해 진화하고 있다.

- _PostgreSQL_: 기본적으로 관계형이지만, 유연한 JSON 데이터 타입을 지원해 구조적·반구조적 저장을 모두 처리 가능.
- _MongoDB_: 문서 저장에 집중했으나, 이제는 강력한 트랜잭션 지원으로 신뢰성과 일관성 강화.
- _Google Spanner_: 관계형 구조와 수평적 확장성, 전 세계적 분산 일관성을 결합한 하이브리드 모델.

```sql
-- 최신 PostgreSQL에서 실제로 동작하는 예시
SELECT users->'profile'->>'twitter_handle'
FROM hybrid_db
JOIN social_graph ON (users->>'id' = social_graph->>'user_id')
WHERE transactions->'amount' > 1000;
```

## 데이터베이스 선택 시 고려사항

- **조직의 필요가 바뀌어도 데이터가 이해하기 쉬울까?**

  _문서형 DB는 진화하는 데이터 모델에 유연하지만, 관계형 DB는 구조 변경이 부담스러울 수 있다._

- **데이터의 연결성이 얼마나 높은가?**

  _높은 연결성은 관계형 모델에, 독립성이 높으면 문서형 모델에 유리하다._

- **데이터 구조를 누가 정의하는가—애플리케이션인가, 데이터베이스인가?**

  _이 결정은 시스템 설계, 확장, 유지보수 방식에 큰 영향을 미친다._

---

## 쿼리 언어

이제 우리가 데이터를 다루는 데 기본이 되는 **쿼리 언어**에 대해 알아보자. 선언적 접근과 명령적 접근의 차이, 웹 개발에서의 활용, 그리고 MapReduce와 같은 분산 시스템에서의 적용까지 살펴본다.

## 선언적 vs. 명령적 쿼리

관계형 데이터베이스의 등장은 단순히 데이터를 저장하는 새로운 방법을 제공한 것이 아니라, 데이터를 질의하는 더 쉬운 방법을 제시했다. SQL은 표준이 되었고, **선언적 쿼리 언어**다. 반면, IMS나 CODASYL 같은 초기 시스템은 **명령적 코드**를 사용했다.

### 차이점은 무엇인가?

아래는 자바스크립트로 데이터셋에서 상어를 찾는 **명령적 코드** 예시다:

```javascript
function getSharks() {
  var sharks = [];
  for (var i = 0; i < animals.length; i++) {
    if (animals[i].family === "Sharks") {
      sharks.push(animals[i]);
    }
  }
  return sharks;
}
```
한 단계씩 컴퓨터에게 어떻게 할지(반복, 조건 확인, 결과 저장)를 지시한다.

이제 **선언적 버전**을 보자:

```sql
SELECT * FROM animals WHERE family = 'Sharks';
```
원하는 결과만 지정하면, 데이터베이스가 알아서 처리 방법을 결정한다.

### 선언적 쿼리의 장점

1. **단순함**: 결과에만 집중할 수 있다.
2. **최적화**: 데이터베이스가 인덱스나 병렬 처리 등 쿼리 실행을 최적화한다.
3. **병렬 실행**: 실행 순서에 덜 의존하므로 여러 코어 또는 머신에서 쉽게 병렬 처리할 수 있다.

## 웹에서의 선언적 쿼리

이 차이는 데이터베이스뿐 아니라 웹 개발에도 적용된다. 예를 들어보자:

```html
<ul>
  <li class="selected">
    <p>Sharks</p>
    <ul>
      <li>Great White Shark</li>
      <li>Tiger Shark</li>
      <li>Hammerhead Shark</li>
    </ul>
  </li>
  <li>
    <p>Whales</p>
    <ul>
      <li>Blue Whale</li>
      <li>Humpback Whale</li>
      <li>Fin Whale</li>
    </ul>
  </li>
</ul>
```
선택된 `<li>`의 `<p>` 요소에 파란색 배경을 주고 싶다면, CSS(선언적)에서는 아래처럼 쓴다:

```css
li.selected > p {
  background-color: blue;
}
```
패턴만 선언하면 된다.

반면, **명령적 자바스크립트**는 다음과 같다:

```javascript
var liElements = document.getElementsByTagName("li");
for (var i = 0; i < liElements.length; i++) {
  if (liElements[i].className === "selected") {
    var children = liElements[i].childNodes;
    for (var j = 0; j < children.length; j++) {
      var child = children[j];
      if (child.nodeType === Node.ELEMENT_NODE && child.tagName === "P") {
        child.setAttribute("style", "background-color: blue");
      }
    }
  }
}
```

### 선언적 접근의 장점

- **더 깔끔한 코드**: CSS가 더 짧고 이해하기 쉽다.
- **동적 업데이트**: `selected` 클래스가 바뀌면 CSS가 자동 처리하지만, JS는 추가 작업이 필요하다.

## MapReduce 쿼리

지금까지 데이터베이스와 웹 개발에서 선언적 vs. 명령적 접근을 살폈다. 이제 분산 시스템의 대표적 모델인 **MapReduce**를 보자. <br>
MapReduce는 구글이 대규모 데이터를 여러 머신에서 처리하기 위해 만든 프로그래밍 모델이다. 완전히 선언적이지도, 명령적이지도 않고 그 중간쯤이다.

### 예시: 상어 관측 수 집계

해양생물학자가 월별 상어 관측 수를 보고 싶다고 하자. <br>
PostgreSQL에서는 다음과 같이 쓴다:

```sql
SELECT date_trunc('month', observation_timestamp) AS observation_month,
       sum(num_animals) AS total_animals
FROM observations
WHERE family = 'Sharks'
GROUP BY observation_month;
```

MongoDB의 MapReduce는 이렇게 쓴다:

```javascript
db.observations.mapReduce(
  function map() {
    var year = this.observationTimestamp.getFullYear();
    var month = this.observationTimestamp.getMonth() + 1;
    emit(year + "-" + month, this.numAnimals);
  },
  function reduce(key, values) {
    return Array.sum(values);
  },
  {
    query: { family: "Sharks" },
    out: "monthlySharkReport"
  }
);
```

- **Map 함수**: 각 문서를 처리해 `"2025-05"`와 `numAnimals` 같은 키-값 쌍을 만든다.
- **Reduce 함수**: 키(월)별로 데이터를 묶어 합계를 계산한다.

### 장단점

- **유연성**: Map/Reduce 함수에 맞춤 로직을 넣을 수 있다.
- **복잡성**: 두 개의 함수를 맞춰 써야 하므로 선언적 쿼리보다 복잡하다.

## 집계 파이프라인(Aggregation Pipeline)

MapReduce의 복잡성을 개선하기 위해 MongoDB는 버전 2.2에서 **집계 파이프라인**을 도입했다. JSON 기반의 선언적 쿼리 언어다.

상어 관측 집계 예시는 다음과 같다:

```javascript
db.observations.aggregate([
  { $match: { family: "Sharks" } },
  { $group: {
      _id: {
        year: { $year: "$observationTimestamp" },
        month: { $month: "$observationTimestamp" }
      },
      totalAnimals: { $sum: "$numAnimals" }
    }
  }
]);
```
집계 파이프라인은 MapReduce보다 더 단순하고 사용하기 쉽다.

## 요약

1. **선언적 쿼리 언어**: "방법"을 감추어 더 쉽게 작성·최적화할 수 있다.
2. **명령적 코드**: 경우에 따라 유용하지만, 대체로 장황하고 유지보수가 어렵다.
3. **MapReduce**: 강력하지만 선언적 대안보다 복잡한 하이브리드 접근.
4. **집계 파이프라인**: 분산 쿼리를 위한 선언적이고 사용자 친화적인 대안.

선언적 쿼리는 코드량을 줄이는 것뿐 아니라, 시스템을 더 똑똑하고 효율적이며 유지보수가 쉽게 만든다. 다음 장에서는 현대 데이터 시스템을 움직이는 도구와 패턴을 계속 탐구한다.

---

## 그래프형 데이터 모델과 쿼리 언어

앞에서는 문서형과 관계형 데이터베이스가 다양한 데이터 관계를 어떻게 처리하는지 살펴봤다. <br>
이제 **복잡하게 연결된 데이터를 모델링할 때 유용한 그래프형 데이터 모델**과 그 쿼리 언어(Cypher, SQL(재귀), SPARQL)를 알아본다.

## 그래프형 데이터 모델

데이터를 모델링할 때, 관계가 핵심이다.

- **일대다** → 문서형 모델
- **다대다** → 관계형 모델
- **복잡한 다대다** → 그래프 모델

그래프는 **연결 자체에 의미가 있을 때** 빛을 발한다.

### 그래프란 무엇인가? 🤔

그래프는 다음으로 구성됩니다:

- **정점(Vertices)**: 노드 또는 엔터티
- **간선(Edges)**: 관계 또는 연결

예시:
- 소셜 그래프: 정점 = 사람, 간선 = 친구 관계
- 웹 그래프: 정점 = 웹페이지, 간선 = 하이퍼링크
- 도로망: 정점 = 교차로, 간선 = 도로

그래프의 강점은 **이질적인 데이터도 한 저장소에 담을 수 있다는 것**입니다.

> 페이스북 그래프에는 사람, 위치, 이벤트, 체크인, 댓글 등이 모두 포함됩니다.  
> 간선은 친구 관계, 체크인 위치, 게시글에 달린 댓글, 이벤트 참석 등을 나타냅니다.

## 예시로 살펴보기

두 사람을 상상해봅시다:

- 루시(Lucy): 미국 아이다호 출신
- 알랭(Alain): 프랑스 보네 출신
- 두 사람은 런던에 살며 결혼함

그래프는 이렇게 표현할 수 있습니다:

- 루시 — 태어난 곳 → 아이다호
- 루시 — 거주지 → 런던
- 알랭 — 태어난 곳 → 보네
- 알랭 — 거주지 → 런던
- 아이다호 — 속함 → 미국
- 보네 — 속함 → 프랑스
- 런던 — 속함 → 잉글랜드 → 유럽

그래프는 루시와 알랭에 대한 더 많은 정보(예: 음식 알레르기)도 손쉽게 확장할 수 있습니다.

> **확장성(Evolvability)**, 이것이 그래프의 장점입니다.

## 프로퍼티 그래프 모델

**정점**은 다음을 가집니다:
- 고유 ID
- 들어오는/나가는 간선 목록
- 속성(Key-Value 쌍)

**간선**은 다음을 가집니다:
- 고유 ID
- 시작 정점(tail)
- 끝 정점(head)
- 레이블(관계 유형)
- 속성(Key-Value 쌍)

아래와 같이 테이블로 구현할 수 있습니다:

```sql
CREATE TABLE vertices (
  vertex_id INTEGER PRIMARY KEY,
  properties JSON
);
CREATE TABLE edges (
  edge_id    INTEGER PRIMARY KEY,
  tail_vertex INTEGER REFERENCES vertices(vertex_id),
  head_vertex INTEGER REFERENCES vertices(vertex_id),
  label       TEXT,
  properties  JSON
);
CREATE INDEX edges_tails ON edges(tail_vertex);
CREATE INDEX edges_heads ON edges(head_vertex);
```

이 구조는 빠른 간선 조회와 다양한 레이블을 한 그래프에 저장할 수 있게 해줍니다.

**중요 포인트:**
- 모든 정점끼리 자유롭게 연결 가능(스키마 제한 없음)
- 어떤 정점이든 들어오는/나가는 간선을 쉽게 찾을 수 있음
- 다양한 관계 레이블을 활용해 한 그래프에 여러 정보를 명확하게 저장 가능

## Cypher 쿼리 언어

Cypher는 Neo4j 그래프 DB를 위한 선언적 쿼리 언어입니다.

생성 예시:

```cypher
CREATE
  (NAmerica:Location {name:'North America', type:'continent'}),
  (USA:Location      {name:'United States', type:'country'}),
  (Idaho:Location    {name:'Idaho', type:'state'}),
  (Lucy:Person       {name:'Lucy'}),
  (Idaho)-[:WITHIN]->(USA)-[:WITHIN]->(NAmerica),
  (Lucy)-[:BORN_IN]->(Idaho);
```

패턴 탐색 예시(MATCH):

```cypher
MATCH
(person) -[:BORN_IN]-> () -[:WITHIN*0..]-> (us:Location {name:'United States'}),
(person) -[:LIVES_IN]-> () -[:WITHIN*0..]-> (eu:Location {name:'Europe'})
RETURN person.name
```

> [:WITHIN*0..] : 0개 이상 WITHIN 간선을 따라가라

**해석:**
- BORN_IN 간선을 따라가면 "United States"에 도달하는 사람
- LIVES_IN 간선을 따라가면 "Europe"에 도달하는 사람

Cypher는 복잡하고 변화하는 스키마, 다대다 관계에 관계형 DB보다 유리합니다.

## SQL의 재귀 CTE

관계형 DB에서 **재귀 CTE(Common Table Expression)**로 그래프 탐색이 가능합니다.  
아래 SQL은 "미국에서 태어나 유럽에 사는 사람"을 찾습니다:

```sql
WITH RECURSIVE
  in_usa(vertex_id) AS (
    SELECT vertex_id FROM vertices WHERE properties->>'name'='United States'
    UNION
    SELECT e.tail_vertex
      FROM edges e JOIN in_usa u ON e.head_vertex=u.vertex_id
     WHERE e.label='within'
  ),
  in_europe(vertex_id) AS (
    SELECT vertex_id FROM vertices WHERE properties->>'name'='Europe'
    UNION
    SELECT e.tail_vertex
      FROM edges e JOIN in_europe eu ON e.head_vertex=eu.vertex_id
     WHERE e.label='within'
  ),
  born_in_usa AS (
    SELECT tail_vertex AS vertex_id
      FROM edges JOIN in_usa ON edges.head_vertex=in_usa.vertex_id
     WHERE edges.label='born_in'
  ),
  lives_in_europe AS (
    SELECT tail_vertex AS vertex_id
      FROM edges JOIN in_europe ON edges.head_vertex=in_europe.vertex_id
     WHERE edges.label='lives_in'
  )
SELECT v.properties->>'name'
  FROM vertices v
  JOIN born_in_usa  b ON v.vertex_id=b.vertex_id
  JOIN lives_in_europe l ON v.vertex_id=l.vertex_id;
```

(동일 목적의 Cypher 쿼리보다 훨씬 길다!)

> **애플리케이션에 맞는 DB를 선택하세요**

## 트리플 스토어 & SPARQL

트리플 스토어는 프로퍼티 그래프 모델과 유사하며, 모든 정보를 **(주어, 술어, 목적어)** 형태의 단순한 3요소로 저장합니다.

- 술어(predicate): 속성 또는 간선
- 목적어(object): 문자열, 숫자 등의 리터럴 또는 다른 정점

예시:
- (lucy, age, 33): lucy라는 정점에 {"age":33} 속성
- (lucy, marriedTo, alain): lucy와 alain이 간선(marriedTo)로 연결됨

Turtle(N3) 예시:

```turtle
@prefix : <urn:example:>.

_:lucy a        :Person;
       :name    "Lucy";
       :bornIn  _:idaho.

_:idaho a       :Location;
       :name    "Idaho";
       :type    "state";
       :within  _:usa.

_:usa a         :Location;
       :name    "United States";
       :type    "country";
       :within  _:namerica.

_:namerica a    :Location;
       :name    "North America";
       :type    "continent".
```

이 예시에서 _:someName은 파일 내에서만 의미가 있고, 술어가 간선이면 목적어는 정점, 속성이면 목적어는 리터럴입니다.
