## MySQL DB-Link ������ ���� FEDERATED ���� Ȱ��ȭ �� ���̺� ����

### 1. ��ġ�Ǿ� �ִ� ���� Ȯ��

![MySQL_DB_link_01.png](./img/MySQL_DB_link_01.png "./img/MySQL_DB_link_01.png")  
	- CentOS���� yum���� ��ġ���� �� �⺻������ ��� ������ �������� ����Դϴ�.

### 2. ������ ����� �� �ֵ��� ��ġ

![MySQL_DB_link_02.png](./img/MySQL_DB_link_02.png "./img/MySQL_DB_link_02.png")

### 3. FEDERATED ������ ��ġ���� Ȯ��

![MySQL_DB_link_03.png](./img/MySQL_DB_link_03.png "./img/MySQL_DB_link_03.png")  
	- FEDERATED ������ ��Ͽ� ǥ�õ����� ��� �������� ���� �����Դϴ�.

### 4. ���� ��� ���� �ϵ��� my.cnf ����

![MySQL_DB_link_04.png](./img/MySQL_DB_link_04.png "./img/MySQL_DB_link_04.png")  
	- [mysqld] ������ federated �׸��� �߰��մϴ�.

### 5. ������ ���¸� Ȯ�� �մϴ�.

![MySQL_DB_link_05.png](./img/MySQL_DB_link_05.png "./img/MySQL_DB_link_05.png")  
	- FEDERATED ������ Support ���°� YES �� ���� �Ǿ����ϴ�.


----------------
## FEDERATED ������ ����Ͽ� ���̺��� �����Ͽ� ������ ���̺�� ����

### 1. �������� ���̺��� �����մϴ�.

	CREATE TABLE `cityholic_db`.`cart_product` (
		`id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '���̵�',
		`users_id` bigint(20) unsigned NOT NULL COMMENT '�����̵�',
		`product_id` bigint(20) NOT NULL COMMENT '��ǰ���̵�',
		`option_code` varchar(50) NOT NULL COMMENT '��ǰ�ɼ��ڵ�',
		`quantity` int(11) NOT NULL DEFAULT '0' COMMENT '��ǰ ����',
		PRIMARY KEY (`users_id`,`product_id`,`option_code `),
		UNIQUE KEY `id_UNIQUE` (`id`)
	) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='īƮ�� ��� ��ǰ';


### 2. ���ÿ� ���̺��� �����մϴ�.

	CREATE TABLE `cityholic_db`.`cart_product` (
		`id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '���̵�',
		`users_id` bigint(20) unsigned NOT NULL COMMENT '�����̵�',
		`product_id` bigint(20) NOT NULL COMMENT '��ǰ���̵�',
		`option_code` varchar(50) NOT NULL COMMENT '��ǰ�ɼ��ڵ�',
		`quantity` int(11) NOT NULL DEFAULT '0' COMMENT '��ǰ ����',
		PRIMARY KEY (`users_id`,`product_id`,`option_code `),
		UNIQUE KEY `id_UNIQUE` (`id`)
	) ENGINE=FEDERATED DEFAULT CHARSET=utf8 COMMENT='īƮ�� ��� ��ǰ'
	CONNECTION='mysql://root:dldusrn1@10.3.0.27:3306/cityholic_db/cart_product';

	- ������ ���̺� Create ������ ENGINE  ����, CONNECTION �ɼ� �߰�  �۾��� ���� �մϴ�.
	- CONNECTION �ɼ��� ������ ������ �����ϴ�.  'mysql://[����]:[��й�ȣ]@[����ip]:[port]/[������DB��]/[������ ���̺��]'


### 3. �̻� ��� ������ �Ϸ� �ߴٸ� ���ÿ��� �������� Table�� ���� ���̺� ó�� ��� �����մϴ�. select, insert, update, delete ��� ���� �մϴ�.


----------
#### References
> [MySQL DB-Link ������ ���� FEDERATED ���� Ȱ��ȭ �� ���̺� ����](http://devse.tistory.com/14 "Hi")  



