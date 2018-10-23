## MySQL DB-Link 구현을 위한 FEDERATED 엔진 활성화 및 테이블 생성

### 1. 설치되어 있는 엔진 확인

![MySQL_DB_link_01.png](./img/MySQL_DB_link_01.png "./img/MySQL_DB_link_01.png")  
	- CentOS에서 yum으로 설치했을 때 기본적으로 사용 가능한 엔진들의 목록입니다.

### 2. 엔진을 사용할 수 있도록 설치

![MySQL_DB_link_02.png](./img/MySQL_DB_link_02.png "./img/MySQL_DB_link_02.png")

### 3. FEDERATED 엔진의 설치여부 확인

![MySQL_DB_link_03.png](./img/MySQL_DB_link_03.png "./img/MySQL_DB_link_03.png")  
	- FEDERATED 엔진이 목록에 표시되지만 사용 가능하지 않은 상태입니다.

### 4. 엔진 사용 가능 하도록 my.cnf 수정

![MySQL_DB_link_04.png](./img/MySQL_DB_link_04.png "./img/MySQL_DB_link_04.png")  
	- [mysqld] 하위에 federated 항목을 추가합니다.

### 5. 엔진의 상태를 확인 합니다.

![MySQL_DB_link_05.png](./img/MySQL_DB_link_05.png "./img/MySQL_DB_link_05.png")  
	- FEDERATED 엔진의 Support 상태가 YES 로 변경 되었습니다.


----------------
## FEDERATED 엔진을 사용하여 테이블을 생성하여 원격지 테이블과 연결

### 1. 원격지에 테이블을 생성합니다.

	CREATE TABLE `cityholic_db`.`cart_product` (
		`id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '아이디',
		`users_id` bigint(20) unsigned NOT NULL COMMENT '고객아이디',
		`product_id` bigint(20) NOT NULL COMMENT '상품아이디',
		`option_code` varchar(50) NOT NULL COMMENT '상품옵션코드',
		`quantity` int(11) NOT NULL DEFAULT '0' COMMENT '상품 개수',
		PRIMARY KEY (`users_id`,`product_id`,`option_code `),
		UNIQUE KEY `id_UNIQUE` (`id`)
	) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='카트에 담긴 상품';


### 2. 로컬에 테이블을 생성합니다.

	CREATE TABLE `cityholic_db`.`cart_product` (
		`id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '아이디',
		`users_id` bigint(20) unsigned NOT NULL COMMENT '고객아이디',
		`product_id` bigint(20) NOT NULL COMMENT '상품아이디',
		`option_code` varchar(50) NOT NULL COMMENT '상품옵션코드',
		`quantity` int(11) NOT NULL DEFAULT '0' COMMENT '상품 개수',
		PRIMARY KEY (`users_id`,`product_id`,`option_code `),
		UNIQUE KEY `id_UNIQUE` (`id`)
	) ENGINE=FEDERATED DEFAULT CHARSET=utf8 COMMENT='카트에 담긴 상품'
	CONNECTION='mysql://root:dldusrn1@10.3.0.27:3306/cityholic_db/cart_product';

	- 원격지 테이블 Create 문에서 ENGINE  수정, CONNECTION 옵션 추가  작업만 수행 합니다.
	- CONNECTION 옵션의 구성은 다음과 같습니다.  'mysql://[계정]:[비밀번호]@[서버ip]:[port]/[원격지DB명]/[원격지 테이블명]'


### 3. 이상 모든 설정을 완료 했다면 로컬에서 원격지의 Table을 로컬 테이블 처럼 사용 가능합니다. select, insert, update, delete 모두 가능 합니다.


----------
#### References
> [MySQL DB-Link 구현을 위한 FEDERATED 엔진 활성화 및 테이블 생성](http://devse.tistory.com/14 "Hi")  



