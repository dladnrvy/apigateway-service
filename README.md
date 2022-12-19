## 설계 내용/이유
- 다량의 트래픽에 대비하여 개별적 scale-out이 가능한 MSA로 아키텍처를 설계하였습니다.
- 분산방법은 Spring cloud를 활용하여 api-gateway 서버를 두고 서비스별로 나누었습니다.
- DB는 분산하지 않았지만, 각 서비스별로 API를 통해 데이터를 주고 받게 개발했습니다. 

## API 명세
 #### 1.barcode
| 메소드 | URI  |설명|
| ------|---- | --- | 
| POST | http://127.0.0.1:8000/barcode/create | 바코드생성 | 
| GET | http://127.0.0.1:8000/barcode/find | 바코드조회 |

 #### 2.partner
| 메소드 | URI  |설명|
| ------|---- | --- | 
| GET | http://127.0.0.1:8000/partner/find | 상점조회 | 

 #### 3.point
| 메소드 | URI  |설명|
| ------|---- | --- | 
| POST | http://127.0.0.1:8000/point/save | 포인트적립 | 
| POST | http://127.0.0.1:8000/point/use  | 포인트사용 |
| GET | http://127.0.0.1:8000/point/result/find  | 내역조회 |

#### TODO
공통
1. kafka 를 통한 DB연결
2. Event Souring 패턴, Saga 패턴등을 통한 트랜잭션 관리 적용

바코드 서버
1. Crockford base-32를 통한 중복하지않는 12자리 코드생성
