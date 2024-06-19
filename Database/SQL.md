# SQL

* 참고 링크: https://www.sqltutorial.org/

## SQL 이란

### SQL 언어 도입

* SQL은 관계형 데이터베이스(RDBMS) 내 데이터를 관리하기 위해 설계 된 프로그래밍 언어

* SQL은 **S**tructured **Q**uery **L**anguage 의 약어

* SQL의 구성 요소

  * **Data Definition Language (DDL)**

    * 데이터 정의 언어
    * 데이터베이스 구조를 설계하는 SQL 명령어 나타냄
    * 데이터베이스 객체를 **만들고**/**수정**
    * 예시: `CREATE` 명령어 사용하여 테이블, 뷰, 인덱스와 같은 DB 객체 생성

  * **Data Manipulation Language (DML)**

    * 데이터 조작 언어
    * 새 정보 쓰거나 RDBMS 기존 레코드 수정
    * 예시: `INSERT` 명령 사용하여 데이터베이스 새 레코드 지정

  * **Data Control Language (DCL)**

    * 데이터 제어 언어
    * DB 액세스를 관리하거나 권한 부여
    * 예시: `GRANT` 명령 사용하여 특정 애플리케이션이 하나 이상 테이블 조작하도록 허용




## SQL 문법

* SQL은 선언형 언어라 문법이 자연어처럼 읽힘

  * SQL 문(statement)은 행위를 묘사하는 **동사**로 시작함
  * 예시: `SELECT`, `INSERT`, `UPDATE`, `DELETE`
  * 동사 이후에는 **주제**와 **술부**가 나옴

* 술부는 `ture` `false` `unknown` 으로 평가될 수 있는 조건으로 특정됨

* 예시

  ```SQL
  SELECT
  		first_name
  FROM
  		employees
  WHERE
  		YEAR(hire_date) = 2000;
  ```

* 위에서 볼 수 있듯이, 보통 문장 처럼 읽힘
  * '2000년에 고용된 고용인의 이름을 가져와라'
* `SELECT first_name`, `FROM employees`, `WHERE` 은 SQL문의 절(clauses)
  * 몇몇 절은 필수
  * `SELECT`, `FROM` 절은 필수
  * `WEHRE` 과 같이 다른 절들은 옵션
* SQL은 기술이 없는 사람들을 염두에 두고 만들어졌기 때문에, 매우 간단하고 쉽게 이해 가능
  * SQL 문을 작성하기 위해
  * PHP, Java, C++과 같은 명령형 언어에서 어떻게 하려는지를 말하기 보다는
  * **무엇**을 할 것인지 말하기만 하면 된다.



### SQL 명령어(commands)

* SQL은 많은 언어로 이루어져 있다.

  * 각 SQL 명령어는 세미콜론 `;` 으로 끝난다.
  * 예를 들어 다음 서로 다른 두 SQL 명령어는 세미콜론으로 구분 된다.

  ```sql
  SELECT
  		first_name, last_name
  FROM
  		employees;
  
  DELETE FROM employees
  WHERE
  		hire_date < '1990-01-01';
  ```

  * SQL은 명령의 끝에 세미콜론을 마킹한다.

* 각 명령어는 리터럴, 키워드, 식별자, 표현문 등의 토큰으로 이루어져 있다.
  * 토큰들은 공백, 탭, 개행 등으로 구분된다.



### 리터럴 Literals

* 리터럴은 상수로 알려진 명백한(explicit) 값이다.

  * SQL은 세 가지 리터럴을 제공한다.
    * string
    * numeric (수)
    * binary

* 문자 리터럴은 따옴표로 감싸진 하나 이상의 알파벳 문자로 이루어져있다.

  ```sql
  'John'
  '1990-01-01'
  '50'
  ```

  * 50은 수지만, 따옴표 `''`로 감싸져있기에 SQL은 이를 문자 리터럴로 다룬다.
  * SQL은 대소문자를 구분한다. 따라서 `'John'` 과 `'JOHN'` 은 다르다.

* 수 리터럴은 정수, 소수, 과학적 표기법 등을 나타낸다.

  ```sql
  200
  -5
  6.0221415E23
  ```

* SQLdms `x'0000'`의 표기법으로 이진값을 표현한다.

  ```sql
  x'01'
  x'0f0ff'
  ```



### 키워드 keywords

* SQL은 특별한 뜻을 가진 많은 키워드들을 가진다.
  * 예: `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `DROP`
  * 이 키워드들은 **예약어**이다.
  * 따라서 이들을 테이블, 컬럼, 인덱스, 뷰, stored procedures, 트리거, 다른 DB 객체 등의 이름으로 사용해서는 안된다.



### 식별자 Identifiers

* 식별자는 테이블, 컬럼, 인덱스 등의 DB 특정 객체를 나타낸다.

  * SQL은 식별자의 대소문자를 구분하지 않는다. (위의 john, JOHN은 달랐지만 여기서는 같다는 뜻)
  * 아래 절들은 모두 같다.

  ```sql
  Select * From employees;
  
  SELECT * FROM EMPLOYEES;
  
  select * from employees;
  
  SELECT * FROM employees;
  ```

* SQL 명령어들의 가독성 향상을 위해 다음과 같은 룰을 따른다. (본 글의 내용에서는)

  * 키워드: uppercase
  * 식별자: lowercase



### 주석 Comments

* SQL 문을 설명하기 위해 SQL 주석을 사용한다.

  * 주석과 함께 SQL 문을 파싱할 때
  * DB 엔진은 주석의 문자열을 무시한다.

* 주석은 연이은 두 하이픈 `--` 으로 나타낸다.

  * 이는 줄의 남은 부분에도 허용된다.

  ```sql
  SELECT
  		employee_id, salary
  FROM
  		employees
  WHERE
  		salary < 3000;-- employess with low salary
  ```

* 여러줄의 설명이 필요할 때는 C 스타일의 표기법 `/**/` 을 사용하면 된다.

  ```sql
  /*
  	increase 5% for employees whose salary is less than 3,000
  	여러줄을 허용한다!
  */
  SELECT
  		employee_id, salary
  FROM
  		employees
  WHERE
  		salary < 3000;
  ```



## 문법 정리

### 예시 사용 테이블

```sql
CREATE TABLE regions (
	region_id INT (11) AUTO_INCREMENT PRIMARY KEY,
	region_name VARCHAR (25) DEFAULT NULL
);

CREATE TABLE countries (
	country_id CHAR (2) PRIMARY KEY,
	country_name VARCHAR (40) DEFAULT NULL,
	region_id INT (11) NOT NULL,
	FOREIGN KEY (region_id) REFERENCES regions (region_id) ON DELETE CASCADE ON UPDATE CASCADE
);

CREATE TABLE locations (
	location_id INT (11) AUTO_INCREMENT PRIMARY KEY,
	street_address VARCHAR (40) DEFAULT NULL,
	postal_code VARCHAR (12) DEFAULT NULL,
	city VARCHAR (30) NOT NULL,
	state_province VARCHAR (25) DEFAULT NULL,
	country_id CHAR (2) NOT NULL,
	FOREIGN KEY (country_id) REFERENCES countries (country_id) ON DELETE CASCADE ON UPDATE CASCADE
);

CREATE TABLE jobs (
	job_id INT (11) AUTO_INCREMENT PRIMARY KEY,
	job_title VARCHAR (35) NOT NULL,
	min_salary DECIMAL (8, 2) DEFAULT NULL,
	max_salary DECIMAL (8, 2) DEFAULT NULL
);

CREATE TABLE departments (
	department_id INT (11) AUTO_INCREMENT PRIMARY KEY,
	department_name VARCHAR (30) NOT NULL,
	location_id INT (11) DEFAULT NULL,
	FOREIGN KEY (location_id) REFERENCES locations (location_id) ON DELETE CASCADE ON UPDATE CASCADE
);

CREATE TABLE employees (
	employee_id INT (11) AUTO_INCREMENT PRIMARY KEY,
	first_name VARCHAR (20) DEFAULT NULL,
	last_name VARCHAR (25) NOT NULL,
	email VARCHAR (100) NOT NULL,
	phone_number VARCHAR (20) DEFAULT NULL,
	hire_date DATE NOT NULL,
	job_id INT (11) NOT NULL,
	salary DECIMAL (8, 2) NOT NULL,
	manager_id INT (11) DEFAULT NULL,
	department_id INT (11) DEFAULT NULL,
	FOREIGN KEY (job_id) REFERENCES jobs (job_id) ON DELETE CASCADE ON UPDATE CASCADE,
	FOREIGN KEY (department_id) REFERENCES departments (department_id) ON DELETE CASCADE ON UPDATE CASCADE,
	FOREIGN KEY (manager_id) REFERENCES employees (employee_id)
);

CREATE TABLE dependents (
	dependent_id INT (11) AUTO_INCREMENT PRIMARY KEY,
	first_name VARCHAR (50) NOT NULL,
	last_name VARCHAR (50) NOT NULL,
	relationship VARCHAR (25) NOT NULL,
	employee_id INT (11) NOT NULL,
	FOREIGN KEY (employee_id) REFERENCES employees (employee_id) ON DELETE CASCADE ON UPDATE CASCADE
);
```

### SELECT

**소개**

* `SELECT` 문은 하나 이상의 테이블에서 데이터를 고른다.

  ```sql
  SELECT
  		select_list
  FROM
  		table_name;
  ```

  * 먼저, `SELECT` 절에서 콤마 `,` 로 구분하여 테이블 컬럼 리스트를 작성한다.
  * 그 다음, `FROM` 절에서 테이블 이름을 특정한다.

* `SELECT` 문을 평가할 때, DB 시스템은 

  * `FROM` 절을 먼저 평가한다.
  * 그 다음 `SELECT` 절을 평가한다.
  * 이는 테이블에서 컬럼들의 데이터를 고르는(select) 것과 같다.

* 세미콜론 `;` 은 쿼리의 일부가 아니다.

  * DB 서버는 두 개의 SQL 절을 구분하는 데 세미콜론을 사용한다.

* 네가 만약 테이블의 모든 컬럼 데이타를 쿼리하고 싶다면

  * 모든 컬럼 이름을 작성하는 대신에,
  * 애스터리스크 `*` 연산자를 사용하면 된다.

  ```sql
  SELECT * FROM table_name;
  ```

* SQL은 케이스를 구분하지 않는다.

  * 따라서, `SELECT` 와 `select` 키워드는 같은 뜻이다.



**예시**

1. 모든 컬럼 데이터 선택하기

   * 아래 예시는 SQL `SELECT` 문을 사용하여 `employees` 테이블의 모든 컬럼과 row의 데이터를 가져오는 것이다.

   ```sql
   SELECT * FROM employees;
   ```

   * `SELECT *` 는 select star로 읽힌다.
     * select star는 ad-hoc 쿼리들에만 유용하다.
   * 애플리케잉션 개발을 위해, 아래와 같은 이유로 select star 사용을 지양해야 한다.
     * select * 는 테이블 모든 컬럼의 데이터를 반환한다. 종종, 애플리케이션은 하나나 약간의 컬럼만 필요하지 모든 컬럼 데이터를 필요로 하지는 않는다.
     * 만약 네가 select * 를 사용한다면, DB는 데이터를 디스크에서 읽고 애플리케이션에 보내는 데까지 더 많은 시간을 필요로 한다. 이는 테이블이 많은 데이터의 많은 컬럼을 포함할 때 좋지 못한 성능의 결과로 이어질 수 있다.

2. 특정 컬럼들에서 데이터 선택하기

   * 특정 컬럼들에서 데이터를 선택하기 위해, `SELECT` 문의 `SELECT` 절 뒤에 컬럼 리스트를 특정할 필요가 있다.
   * 예를 들어, 아래 예시는 `employees` 테이블의 employee id, first name, last name, hire date 모든 row를 선택한다.

   ```sql
   SELECT
   		employee_id,
   		first_name,
   		last_name,
   		hire_date
   FROM
   		employees;
   ```

3. 간단한 계산 수행하기

   * 아래 예시는 `SELECT` 문을 사용하여 first name, last name, salary, new salary를 가져오는 것이다.

   ```sql
   SELECT
   		first_name,
   		last_name,
   		salary,
   		salary * 1.05
   FROM
   		employees;
   ```

   * `salary * 1.05` 식은 모든 고용자들의 급여에 5%를 추가한다.
   * 기본적으로, SQL은 식을 컬럼 헤딩에 사용한다.
   * 식이나 컬럼을 alias에 할당하기 위해, `AS` 키워드를 사용하여 아래와 같이 작성할 수 있다.

   ```sql
   expression AS column_alias
   ```

   * 예를 들어, 아래 `SELECT` 문에서 `new_salary` 컬럼 alias로 사용되고 `salary * 1.05` 가 할당된다.

   ```sql
   SELECT
   		first_name,
   		last_name,
   		salary,
   		salary * 1.05 AS new_salary
   FROM
   		employees;
   ```



**정리**

* 테이블에서 데이터를 선택하기 위해 SQL `SELECT` 문을 사용하자
* 테이블에서 데이터를 선택하기 위해, `FROM` 절에 테이블 이름을 특정하고 `SELECT` 절에 컬럼 리스트를 작성하자
* `SELECT *` 는 테이블의 모든 컬럼을 `SELECT` 하는 약어이다.



### ORDER BY

**소개**

* `ORDER BY` 는 `SELECT` 문의 선택 절이다.

  * `ORDER BY` 절을 사용하여 `SELECT` 절에서 반환하는 행을 오름차순 혹은 내림차순으로 정렬할 수 있다.

  ```sql
  SELECT
  		select_list
  FROM
  		table_name
  ORDER BY
  		sort_expression [ASC | DESC]
  ```

  * 이 문법을 풀어 설명하면,
    * 첫째, `ORDER BY` 절을 `FROM` 절 뒤에 배치한다. DB는 `SELECT` 문을 `ORDER BY` * 절을 `FROM` > `SELECT` > `ORDER BY` 의 순서대로 평가할 것이다.
    * 둘째, `ORDER BY` 절 뒤에 정렬 식을 특정한다. 정렬식은 정렬 기준으로 특정된다.
    * 셋째, `ASC` 옵션은 오름차순으로, `DESC` 옵션은 내림 차순으로 정렬한다.
  * `ORDER BY` 는 `ASC` 옵션을 default 로 사용함에 주목하자.
  * `ORDER BY` 절은 또한 여러개의 식으로 정렬될 수 있다. 이 경우 콤마 `,` 로 두 식을 구분해야 한다.

  ```sql
  SELECT
  		select_list
  FROM
  		table_name
  ORDER BY
  		sort_expression_1 [ASC | DESC]
  		sort_expression_2 [ASC | DESC]
  ```

  * 이 문법에서, `ORDER BY` 절은 `sort_expression_1` 로 먼저 정렬된다. 그 다음 `sort_expression_2` 로 정렬된다.
  * 만약 `ORDER BY` 절을 특정하지 않는다면, `SELECT` 문은 결과 셋을 정렬하지 않는다. 이는 결과의 row들이 특정 순서를 가지지 않는다는 뜻이다.



**예시**

1. 하나의 컬럼 정렬하기

   * 아래 예시는 `SELECT` 문을 사용하여 employee id, first name, last name, hire date, salary 등을 `employees` 테이블에서 가져오는 것이다.

   ```sql
   SELECT
   		employee_id,
   		first_name,
   		last_name,
   		hire_date,
   		salary
   FROM
   		employees;
   ```

   ```
   +-------------+-------------+-------------+------------+----------+
   | employee_id | first_name  | last_name   | hire_date  | salary   |
   +-------------+-------------+-------------+------------+----------+
   |         100 | Steven      | King        | 1987-06-17 | 24000.00 |
   |         101 | Neena       | Kochhar     | 1989-09-21 | 17000.00 |
   |         102 | Lex         | De Haan     | 1993-01-13 | 17000.00 |
   |         103 | Alexander   | Hunold      | 1990-01-03 |  9000.00 |
   |         104 | Bruce       | Ernst       | 1991-05-21 |  6000.00 |
   |         105 | David       | Austin      | 1997-06-25 |  4800.00 |
   |         106 | Valli       | Pataballa   | 1998-02-05 |  4800.00 |
   |         107 | Diana       | Lorentz     | 1999-02-07 |  4200.00 |
   |         108 | Nancy       | Greenberg   | 1994-08-17 | 12000.00 |
   |         109 | Daniel      | Faviet      | 1994-08-16 |  9000.00 |
   |         110 | John        | Chen        | 1997-09-28 |  8200.00 |
   ...
   ```

   * 결과를 보면 알 수 있듯이, 어떠한 정렬도 가지고 있지 않다.
   * 아래 예시는 `ORDER BY` 절을 사용하여 고용인들의 이름으로 정렬한다. (오름차순)

   ```sql
   SELECT
   		employee_id,
   		first_name,
   		last_name,
   		hire_date,
   		salary
   FROM
   		employees
   ORDER BY
   		first_name;
   ```

   ```
   +-------------+-------------+-------------+------------+----------+
   | employee_id | first_name  | last_name   | hire_date  | salary   |
   +-------------+-------------+-------------+------------+----------+
   |         121 | Adam        | Fripp       | 1997-04-10 |  8200.00 |
   |         115 | Alexander   | Khoo        | 1995-05-18 |  3100.00 |
   |         103 | Alexander   | Hunold      | 1990-01-03 |  9000.00 |
   |         193 | Britney     | Everett     | 1997-03-03 |  3900.00 |
   |         104 | Bruce       | Ernst       | 1991-05-21 |  6000.00 |
   |         179 | Charles     | Johnson     | 2000-01-04 |  6200.00 |
   |         109 | Daniel      | Faviet      | 1994-08-16 |  9000.00 |
   |         105 | David       | Austin      | 1997-06-25 |  4800.00 |
   |         114 | Den         | Raphaely    | 1994-12-07 | 11000.00 |
   |         107 | Diana       | Lorentz     | 1999-02-07 |  4200.00 |
   ...
   ```

   * `ORDER BY` 는 `first_name` 컬럼의 값을 정렬한다.

2. 여러 컬럼 값 정렬하기

   * 아래 예시는 `ORDER BY` 절을 사용해 이름을 오름차순으로 정렬하고 성을 내림차순으로 정렬한 것이다.

   ```sql
   SELECT
   		employee_id,
   		first_name,
   		last_name,
   		hire_date,
   		salary
   FROM
   		employees
   ORDER BY
   		first_nanem
   		last_nane DESC;
   ```

   ```
   +-------------+-------------+-------------+------------+----------+
   | employee_id | first_name  | last_name   | hire_date  | salary   |
   +-------------+-------------+-------------+------------+----------+
   |         121 | Adam        | Fripp       | 1997-04-10 |  8200.00 |
   |         115 | Alexander   | Khoo        | 1995-05-18 |  3100.00 |
   |         103 | Alexander   | Hunold      | 1990-01-03 |  9000.00 |
   |         193 | Britney     | Everett     | 1997-03-03 |  3900.00 |
   |         104 | Bruce       | Ernst       | 1991-05-21 |  6000.00 |
   |         179 | Charles     | Johnson     | 2000-01-04 |  6200.00 |
   |         109 | Daniel      | Faviet      | 1994-08-16 |  9000.00 |
   |         105 | David       | Austin      | 1997-06-25 |  4800.00 |
   |         114 | Den         | Raphaely    | 1994-12-07 | 11000.00 |
   |         107 | Diana       | Lorentz     | 1999-02-07 |  4200.00 |
   |         118 | Guy         | Himuro      | 1998-11-15 |  2600.00 |
   ...
   ```

   * 이 예시에서, `ORDER BY` 절은 이름을 오름차순으로 정렬 한 뒤, 성을 기준으로 내림차순 정렬한다.
   * `Alexander Khoo` 와 `Alexander Hunold` 의 순서가 바뀐 것에 주목하자

3. 수 컬럼의 값 정렬하기

   * 아래 예시는 `ORDER BY` 절을 사용하여 임금을 내림차순으로 정렬한 것이다.

   ```sql
   SELECT
   		employee_id,
   		first_name,
   		last_name,
   		hire_Date,
   		salary
   FROM
   		employees
   ORDER BY
   		salary DESC;
   ```

   ```
   +-------------+-------------+-------------+------------+----------+
   | employee_id | first_name  | last_name   | hire_date  | salary   |
   +-------------+-------------+-------------+------------+----------+
   |         100 | Steven      | King        | 1987-06-17 | 24000.00 |
   |         101 | Neena       | Kochhar     | 1989-09-21 | 17000.00 |
   |         102 | Lex         | De Haan     | 1993-01-13 | 17000.00 |
   |         145 | John        | Russell     | 1996-10-01 | 14000.00 |
   |         146 | Karen       | Partners    | 1997-01-05 | 13500.00 |
   |         201 | Michael     | Hartstein   | 1996-02-17 | 13000.00 |
   |         205 | Shelley     | Higgins     | 1994-06-07 | 12000.00 |
   |         108 | Nancy       | Greenberg   | 1994-08-17 | 12000.00 |
   |         114 | Den         | Raphaely    | 1994-12-07 | 11000.00 |
   ...
   ```

4. 날짜 정렬하기

   * 문자와 숫자 데이터 외에, `ORDER BY` 절을 사용하여 날짜 정렬도 가능하다.
   * 예를 들어, 아래 절은 `ORDER BY` 절을 사용하여 `hire_date` 기준으로 정렬한 것이다.

   ```sql
   SELECT
   		employee_id,
   		first_name,
   		last_name,
   		hire_date,
   		salary
   FROM
   		employees
   ORDER BY
   		hire_date;
   ```

   ```
   +-------------+-------------+-------------+------------+----------+
   | employee_id | first_name  | last_name   | hire_date  | salary   |
   +-------------+-------------+-------------+------------+----------+
   |         100 | Steven      | King        | 1987-06-17 | 24000.00 |
   |         200 | Jennifer    | Whalen      | 1987-09-17 |  4400.00 |
   |         101 | Neena       | Kochhar     | 1989-09-21 | 17000.00 |
   |         103 | Alexander   | Hunold      | 1990-01-03 |  9000.00 |
   |         104 | Bruce       | Ernst       | 1991-05-21 |  6000.00 |
   |         102 | Lex         | De Haan     | 1993-01-13 | 17000.00 |
   |         203 | Susan       | Mavris      | 1994-06-07 |  6500.00 |
   |         204 | Hermann     | Baer        | 1994-06-07 | 10000.00 |
   ...
   ```

   * 최신순으로 정렬하고 싶다면, 날짜를 내림차순으로 정렬하면 된다.

   ```sql
   SELECT
   		employee_id,
   		first_name,
   		last_name,
   		hire_date,
   		salary
   FROM
   		employees
   ORDER BY
   		hire_date DESC;
   ```



**정리**

* `SELECT` 절에서 반환된 row들을 정렬하기 위해서 `ORDER BY` 절을 사용하자
* 오름차순은 `ASC` , 내림차순은 `DESC` 옵션을 사용해 정렬하자



### DISTINCT

**소개**

* 결과 셋에서 중복되는 row를 제거하기 위해서 `DISTINCT` 연산자를 사용하자

  ```sql
  SELECT DISTINCT
  		column1, column2, ...
  FROM
  		table1;
  ```

  * `DISTINCT` 연산자 뒤에 컬럼을 사용하면, `DISTINCT` 연산자는 컬럼의 값들을 중복 평가에 사용한다.
  * 두 개 이상의 컬럼을 사용한다면, `DISTINCT` 는 그 컬럼들의 값들의 조합을 중복 평가에 사용한다.

  > `DISTINCT` 는 결과 셋에서 중복을 제거할 뿐이지, 테이블에서 중복을 삭제하지는 않는다.

* 만일 두개의 컬럼을 고르면서 하나의 컬럼에 대해서만 중복 제거를 하고 싶다면, `GROUP BY` 문을 사용하자



**예시**

1. 한개의 컬럼에 대한 연산

   * 아래 문은 `employees` 테이블에서 임금 컬럼의 데이터를 가져온 뒤 내림차순으로 정렬한 것이다.

   ```sql
   SELECT
   		salary
   FROM
   		employees
   ORDER BY salary DESC;
   ```

   ```
   +----------+
   | salary   |
   +----------+
   | 24000.00 |
   | 17000.00 |
   | 17000.00 |
   | 14000.00 |
   | 13500.00 |
   | 13000.00 |
   | 12000.00 |
   | 12000.00 |
   | 11000.00 |
   | 10000.00 |
   |  9000.00 |
   |  9000.00 |
   ...
   ```

   * 결과는 중복을 가지고 있다. (17000, 12000, 9000)
   * 아래 문은 `DISTINCT` 연산자를 사용해 유니크 값을 찾아낸다.

   ```sql
   SELECT
   		DISTINCT salary
   FROM
   		employees
   ORDER BY salary DESC;
   ```

   ```
   +----------+
   | salary   |
   +----------+
   | 24000.00 |
   | 17000.00 |
   | 14000.00 |
   | 13500.00 |
   | 13000.00 |
   | 12000.00 |
   | 11000.00 |
   | 10000.00 |
   |  9000.00 |
   ```

2. 여러 컬럼에서의 연산

   * 아래 문은 job id와 salary를 `employees` 테이블에서 가져온다.

   ```sql
   SELECT
   		job_id,
   		salary
   FROM
   		employees
   ORDER BY
   		job_id,
   		salary DESC;
   ```

   ```
   +--------+----------+
   | job_id | salary   |
   +--------+----------+
   |      1 |  8300.00 |
   |      2 | 12000.00 |
   |      3 |  4400.00 |
   |      4 | 24000.00 |
   |      5 | 17000.00 |
   |      5 | 17000.00 |
   |      6 |  9000.00 |
   |      6 |  8200.00 |
   ...
   ```

   * 결과를 보면, 몇몇 중복이 있음을 확인할 수 있다. 이는 두명의 고용인이 같은 job id와 salary를 가지고 있음을 의미한다.
   * 아래 문은 `DISTINCT` 연산자를 사용해 job id와 salary 중복을 제거한다.

   ```sql
   SELECT DISTINCT
   		job_id,
   		salary
   FROM
   		employees
   ORDER BY
   		job_id,
   		salary DESC;
   ```

   ```
   +--------+----------+
   | job_id | salary   |
   +--------+----------+
   |      1 |  8300.00 |
   |      2 | 12000.00 |
   |      3 |  4400.00 |
   |      4 | 24000.00 |
   |      5 | 17000.00 |
   |      6 |  9000.00 |
   |      6 |  8200.00 |
   ...
   ```

   * job id에 여전히 중복이 존재한다. 이는 `DISTINCT` 연산자를 `job_id` 와 `salary` 둘에 적용했기 때문이다. 이렇게 되면 `job_id` 의 중복이 아니라, `job_id` `salary` 두 개 모두 중복되는 것만 제거한다.

3. NULL에 관하여

   * DB에서, `NULL`은 unknown이나 missing data를 의미한다.
   * 수, 문자열, 날짜 등의 값과 달리, `NULL`은 그 어떤것과도 같지 않다. 심지어는 자기 자신과도 같지 않다. 아래 표현식은 `unknown`이나 `NULL` 을 반환할 것이다.

   ```sql
   NULL=NULL
   ```

   * 보통, `DISTINCT` 연산자는 모든 `NULL` 을 동일하게 취급한다. 그러므로, `DISTINCT` 연산자는 결과 셋에서 딱 하나의 `NULL` 만 남길 것이다.

   > 이 행위는 DB 제품에 따라 달라질 수 있다.

   * 예를 들어, 아래 문은 구별되는(중복이 없는) 핸드폰 번호를 반환한다.

   ```sql
   SELECT DISTINCT phone_number
   FROM emplyees
   ORDER BY phone_number;
   ```

   ```
   +--------------+
   | phone_number |
   +--------------+
   | NULL         |
   | 515.123.4444 |
   | 515.123.4567 |
   | 515.123.4568 |
   | 515.123.4569 |
   | 515.123.5555 |
   ...
   ```

   * 하나의 `NULL` 만 반환되는 점에 주목하자



**정리**

* 중복 제거를 위해서는 `DISTINCT` 연산자를 사용하자



### LIMIT

**소개**

* `SELECT` 문에서 제한된 수의 row만 반환받고 싶다면 `LIMIT`와 `OFFSET` 절을 사용하자

  ```sql
  SELECT
  		column_list
  FROM
  		table1
  ORDER BY column_list
  LIMIT row_count OFFSET offset;
  ```

  * 이 문법에서
    * `LIMIT row_count`는 `row_count` 의 줄만큼 row를 반환하게 한다.
    * `OFFSET offset` 절은 `offset`의 row만큼 스킵 한 뒤 반환한다.
  * `OFFSET` 문은 옵션이다. 이걸 빼도 쿼리는 `row_count` 만큼의 row를 반환한다.
  * `LIMIT` 문 사용 시, 결과 셋의 row 순서를 보장하기 위해 `ORDER BY` 문을 사용함은 중요하다.
  * 모든 DB 시스템이 `LIMIT` 문을 지원하지 않는다. 그러므로 `LIMIT` 문은 MySQL, PostgreSQL, SQLite 등의 DB 시스템에서만 지원한다. 만약 SQL Server를 사용한다면 `SELECT TOP` 을 대신 사용하자.



**예시**

1. 기초

   * 다음 예시는 `LIMIT` 절을 사용해 처음 5개 row만 가져오는 것이다.

   ```sql
   SELECT
   		employee_id,
   		first_name,
   		last_name
   FROM
   		employees
   ORDER BY
   		first_name
   LIMIT 5;
   ```

   * 다음 예시는 `LIMIT` , `OFFSET` 둘 다 사용해 4번째 줄부터 5개 row를 가져오는 것이다.

   ```sql
   SELECT
   		emplyee_id, first_name, last_name
   FROM
   		employees
   ORDER BY first_name
   LIMIT 5 OFFSET 3;
   ```

   * MySQL에서는 다음과 같이 줄여 쓸 수 있다.

   ```sql
   LIMIT 3, 5;
   ```

2. 가장 높거나 낮은 N 개의 row 가져오기

   * `LIMIT` 절을 사용해 가장 높거나 낮은 값 N 개 row를 가져올 수 있다. 예를 들어, 다음 문은 가장 높은 임금을 받는 5명의 고용인을 가져오는 것이다.

   ```sql
   SELECT
   		employee_id,
   		first_name,
   		last_name,
   		salary
   FROM
   		employees
   ORDER BY
   		salary DESC
   LIMIT 5;
   ```

   * 먼저 `ORDER BY` 절은 고용인을 임금 내림차순으로 정렬한다. 그 다음 `LIMIT` 절이 쿼리로부터 반환받은 row를 5개로 제한한다.

3. N 번째로 높은 값 가져오기

   * 회사에서 두 번째로 높은 임금을 받는 고용인을 뽑으려면, `LIMIT OFFESET` 을 다음과 같이 사용하면 된다.

   ```sql
   SELECT
   		employee_id,
   		first_name,
   		last_name,
   		salary
   FROM
   		employees
   ORDER BY
   		salary DESC
   LIMIT 1 OFFSET 1;
   ```

   * `ORDER BY` 절은 고용인들을 임금 기준 내림차순으로 정렬한다. 그리고 `LIMIT 1 OFFSET 1` 절은 결과 셋에서 두 번째 row를 가져온다.
   * 이 쿼리는 모든 고용인이 서로 다른 임금을 받고 있다는 가정하에 작동한다. 두명의 고용인이 같은 임금을 받고 있다면 올바르게 작동하지 않을 것이다.
   * 또한, 두 번째로 높은 임금을 받는 사람이 두 명 이상이라면, 쿼리는 첫번째 사람만 반환할 것이다.
   * 이 이슈를 해결하려면 다음과 같이 해보자

   ```sql
   SELECT DISTINCT
   		salary
   FROM
   		employees
   ORDER BY salary DESC
   LIMIT 1, 1;
   ```

   * 이처럼 중복을 제거한 임금 값 중 두번째로 높은 값을 추출 한 뒤 (결과값 17000)

   ```sql
   SELECT
   		emplyee_id, first_name, last_name, salary
   FROM
   		emplyees
   WHERE
   		salary = 17000;
   ```

   * 추출값을 쿼리에 삽입하자
   * 서브쿼리에 대해 알고 있다면, 두 쿼리를 하나의 쿼리로 합칠 수 있다.

   ```sql
   SELECT
   		emplyee_id, first_name, last_name, salary
   FROM
   		emplyees
   WHERE
   		salary = (SELECT DISTINCT
                	salary
                FROM
                 emplyees
                ORDER BY salary DESC
                LIMIT 1, 1);
   ```



**정리**

* `LIMIT` & `OFFSET` 을 사용해 쿼리 반환값의 row 수를 제한할 수 있다.
* `LIMIT` & `OFFSET` 은 SQL 표준이 아니다.



### FETCH

**소개**

* 쿼리 반환값에서 row의 수를 제한하기 위해 `LIMIT` 절을 사용한다.

  * `LIMIT` 절은 많은 DB 시스템에서 지원한다.
  * 하지만 SQL 표준은 아니다.

* SQL:2008은 `OFFSET FETCH` 절을 `LIMIT` 문과 비슷한 기능으로 소개한다.

  * `OFFSET FETCH` 절을 사용하여 row 반환 전 결과 셋의 첫 번째 `N` 개 행을 건너뛸 수 있다.

  ```sql
  OFFSET offset_rows { ROW | ROWS }
  FETCH { FIRST | NEXT } [ fetch_rows ] { ROW | ROWS } ONLY
  ```

  * 이 문법에서
    * `ROW` 와 `ROWS`, `FIRST` 와 `NEXT` 는 동의어이다. 그러므로, 서로 상호교환 가능하다.
    * `offset_rows`는 0 이상의 정수이다. `offset_rows`가 결과 셋 줄 수보다 클 경우, 아무 row도 반환되지 않는다.
    * `fetch_rows` 또한 정수이며 반환될 row의 수를 결정한다. `fetch_rows` 값은 1 이상이다.
  * row들은 정렬되지 않은 상태로 테이블에 저장되어 있기 때문에, 매번 동일한 결과를 얻기 위해서는 `ORDER BY` 절과 함께 사용해야 한다.

* 많은 DB 시스템은 `OFFSET FETCH` 절을 지원한다. 그러나 각 DB 시스템은 `OFFSET FETCH` 절을 조금 다른 방식으로 실행한다.

* `OFFSET FETCH` 절은 보통 페이지네이션을 요구하는 클라이언트나 웹 애플리케이션에서 사용된다.

  * 예를 들어, 각 페이지가 10개 row를 가질 때, 두 번째 페이지를 얻기 위해서 쿼리에서 첫 10개 row를 스킵할 수 있다.



**예시**

* 아래 예시는 가장 높은 임금을 가진 고용인을 반환한다.

  ```sql
  SELECT
  		employee_id,
  		first_name,
  		last_name,
  		salary
  FROM employees
  ORDER BY
  		salary DESC
  OFFSET 0 ROWS
  FETCH NEXT 1 ROWS ONLY;
  ```

  * 먼저 `ORDER BY` 절은 고용인 목록을 임금 내림차순으로 정렬한다.
  * `OFFSET` 절은 `0 ROWS` 이므로 아무것도 스킵하지 않는다.
  * `FETCH` 절은 위에서 첫번째 row만 반환한다.

* 다음 예시는 고용인 목록을 임금순으로 정렬하고, 가장 높은 임금 5명을 스킵한 뒤, 그 다음 5명을 가지고 오는 것이다.

  ```sql
  SELECT
  		employee_id,
  		first_name,
  		last_name,
  		salary
  FROM employees
  ORDER BY
  		salary DESC
  OFFSET 5 ROWS
  FETCH NEXT 5 ROWS ONLY;
  ```

  

**정리**

* 쿼리에서 반환된 rows 중 제한된 줄만 가져오고 싶다면 `FETCH` 를 사용하자
* `FETCH` 절은 N 줄 만큼 스킵하고 그 다음부터의 줄들을 가져온다.



### WHERE

**소개**

* 테이블에서 특정 row들을 선택하기 위해서 `SELECT` 문에서 `WHERE` 절을 사용하면 된다.

  ```sql
  SELECT
  		column1, column2, ...
  FROM
  		table_name
  WHERE
  		condition;
  ```

  * `WHERE` 절은 `FROM` 절 바로 뒤에 나온다.
  * `WHERE` 절은 하나 이상의 테이블의 각 row를 평가하는 논리 표현식을 포함한다.
  * 조건 평가에서 true라면 결과 셋에 포함되고 그렇지 않다면 배제된다.

* SQL은 three-valued logic 임에 주목할 필요가 있다. three-valued logic 은 3개의 가능한 논리가 있다는 뜻이다. 3개의 가능 논리에는 TRUE, FALSE, UNKOWN이 있다.

  * 이는 조건이 FALSE나 NULL로 평가된다면 해당 row는 결과 셋에 포함되지 않음을 의미한다.

* `WEHRE` 절 뒤에 오는 논리 표현식은 술부로 알려져 있다.

  * `WHERE` 절에 사용하는 row 선택 기준을 형성하기 위해 다양한 연산자를 사용할 수 있다.

* 아래는 SQL 비교 연산자이다.

  * `=` - 같음
  * `<> (!=)` - 다름
  * `<` - 작음
  * `>` - 큼
  * `<=` - 작거나 같음
  * `>=` - 크거나 같음

* 같단한 표현식 구성을 위해 두개의 피연산자와 위에 나온 연산자를 사용할 수 있다.

  ```sql
  salary > 1000
  ```

  * 이는 **봉급이 1000 초과인가요?** 라고 묻는 것이다.

  ```sql
  min_salary < max_salary
  ```

  * 이 표현식은 **"가장 낮은 임금이 가장 큰 임금보다 작나요?"**라고 묻는 것이다.

* 표현식에 사용되는 리터럴 값은 숫자, 문자, 날짜, 시간 등을 사용할 수 있다.

  * 숫자: 정수나 소수를 사용할 수 있다. (예: 100, 200.5)
  * 문자: 홑따옴표, 쌍따옴표 등을 사용해서 표현할 수 있다. (예: "100", "John")
  * 날짜: DB에 맞는 형식을 사용한다. (예: MySQL은 'yyyy-mm-dd'의 형식을 사용한다)
  * 시간: DB에 맞는 형식을 사용한다. (예: MySQL은 'HH:MM:SS' 의 형식을 사용한다)

* `SELECT` 문 외에, `WHERE` 절은 `UPDATE`, `DELETE` 문에도 특정 rows를 업데이트 하거나 삭제하는 데 사용할 수 있다.



**예시**

1. 숫자 비교하기

   * 아래 예시는 고용인 중 임금이 14,000 보다 높은 사람들을 뽑고 결과 셋을 내림차순으로 정렬하는 것이다.

   ```sql
   SELECT
   		employee_id,
   		first_name,
   		last_name,
   		salary
   FROM
   		employees
   WHERE
   		salary > 14000
   ORDER BY
   		salary DESC;
   ```

   * 아래 쿼리는 id가 5인 부서에서 일하는 고용인들을 뽑는다.

   ```sql
   SELECT
   		...
   FROM
   		employees
   WHERE
   		department_id = 5
   ORDER BY
   		first_name;
   ```

   

2. 문자로 `WHERE` 쓰기

   * SQL은 case를 구분하지 않는다. 그러나 비교 구문에서는 case를 구분한다.
   * 예를들어, 아래 예시는 성이 `Chen` 인 사람을 찾는다.

   ```sql
   SELECT ...
   FROM emplyees
   WHERE last_name = 'Chen'
   ```

   * 위 예시에서 `CHEN` 이나 `chen` 을 사용한다면 어떤 결과값도 나오지 않을 것이다.



3. 날짜와 `WHERE` 쓰기

   * `1999년 1월 1일` 이후 입사한 고용인들을 뽑기 위해, 아래 쿼리를 사용해보자

   ```sql
   SELECT ...
   FROM emplyees
   WHERE
   		hire_date >= '1999-01-01'
   ORDER BY hire_date DESC;
   ```

   * 만일 1999년 입사한 고용인들을 찾고 싶다면 몇 가지 방법이 있다.
     1. `YEAR` 함수를 사용하여 `hire_date` 컬럼에서 연도를 뽑고 동등 연산자 `=`를 사용하자
     2. `AND` 연산자와 두 표현식을 사용하자
     3. `BETWEEN` 연산자를 사용하자
   * 아래 문은 첫 번째 방법을 구현한다.

   ```sql
   SELECT ...
   FROM emplyees
   WHERE
   		YEAR (hire_Date) = 1999
   ORDER BY
   		hire_date DESC;
   ```

   

### Comparison Operators

* SQL 비교연산자는 두 표현식을 테스트 할 수 있다.
* 비교 연산자 종류는 아래와 같다.
  * `=` - 같음
  * `<>` - 같지 않음 (다름)
  * `>` - 큼
  * `>` - 크거나 같음
  * `<` - 작음
  * `<=` - 작거나 같음
* 비교 연산자의 결과는 `true`, `false`, `unknown` 등 세 가지이다.



**동등 연산자 `=`**

* 동등 연산자는 두 표현식이 같은 지 비교한다.

  ```sql
  expression1 = expression2
  ```

  * 위 식은 왼쪽 표현식의 값이 오른쪽 표현식과 같다면 `true` 를 반환하고, 다르다면 `false` 를 반환한다.
  * 예를 들어, 아래 문은 성이 `Himuro` 인 사람을 찾는다.

  ```sql
  SELECT ...
  FROM emplyees
  WHERE last_name = 'Himuro';
  ```

  * 이 예시에서, 쿼리는 `employees` 테이블의 `last_name` 컬럼에서 `Himuro` 문자열을 찾는다.

* 동등 연산자는 null 값을 비교할 수 없다.

  * 예를 들어, 다음 쿼리는 핸드폰 번호가 없는 모든 고용인을 찾는다.

  ```sql
  SELECT ...
  FROM emplyees
  WHERE
  		phone_number = NULL;
  ```

  * 그러나 위 쿼리는 빈 결과 셋을 반환한다.
  * 다음 표현식은 항상 `false` 를 반환하기 때문이다.

  ```sql
  phone_number = NULL
  ```

  * null 값을 비교하기 위해 `IS NULL` 연산자를 사용해야 한다.

  ```sql
  SELECT ...
  FROM emplyees
  WHERE
  		phone_number IS NULL;
  ```



**부등 연산자 `<>`**

* 부등 연산자는 null이 아닌 표현식들을 비교하고 왼쪽 표현식과 오른쪽 표현식 값이 다르다면 `true` 를 반환한다.

  ```sql
  expression1 <> expression2
  ```

  * 예를 들어, 아래 문은 부서 id 가 8이 아닌 모든 고용인들을 뽑는다.

  ```sql
  SELECT ...
  FROM emplyees
  WHERE department_id <> 8
  ORDER BY first_name, last_name;
  ```

* 또한 `AND` 연산자를 활용하여 `<>` 연산자를 사용하는 여러개의 표현식을 묶을 수도 있다.

  * 예를 들어, 아래 문은 부서 id가 8과 10이 아닌 모든 고용인을 뽑는다.

  ```sql
  SELECT ...
  FROM emplyees
  WHERE
  		department_id <> 8
  				AND department_id <> 10
  ORDER BY first_name, last_name;
  ```

  

**큼 연산자 `>`**

* 큼 연산자는 null이 아닌 두 표현식을 비교하여, 왼쪽 피연산자가 오른쪽 피연산자보다 크다면 `true` 를, 작다면 `false` 를 반환한다.

  ```sql
  expression1 > expression2
  ```

  * 예를 들어, 임금이 10,000 보다 높은 고용인을 찾기 위해 `WHERE` 문에 큼 연산자를 사용할 수 있다.

  ```sql
  SELECT ...
  FROM emplyees
  WHERE salary > 10000
  ORDER BY salary DESC;
  ```

  * `AND` 나 `OR` 연산자를 사용하여 다양한 연산자를 사용하는 표현식을 합칠 수 있다.
  * 얘를 들어, 아래 문은 부서 8에서 일하면서 임금이 10,000이 넘는 사람을 찾는 것이다.

  ```sql
  SELECT ...
  FROM emplyees
  WHERE
  		salary > 10000 AND department_id = 8
  ORDER BY salary DESC;
  ```



**작음 연산자 `<`**

* 큼 연산자와 반대로 왼쪽 피연산자가 오른쪽 피연산자보다 **작다면** `true` 를 반환한다.

  ```sql
  expression1 < expression2
  ```

  * 예를 들어, 아래 문은 임금이 10,000 보다 낮은 모든 고용자들을 뽑는다.

  ```sql
  SELECT ...
  FROM emplyees
  WHERE salary < 10000
  ORDER BY salary DESC;
  ```

  

### Logical Operators

* 논리 연산자(logical operator)는 조건이 참인지 테스트하기 위해 사용된다.
  * 비교 연산자와 비슷하게, 논리 연산자도 `true`, `false`, `unknown` 을 반환한다.
* 아래는 논리 연산자 목록이다.
  * `ALL` - 모든 비교가 `true` 라면 `true` 반환
  * `AND` - 양쪽 모두 `true` 라면 `true` 반환
  * `ANY` - 어느 한 비교만 `true` 여도 `true` 반환
  * `BETWEEN` - 피연산자가 범위 내라면 `true` 반환
  * `EXISTS` - 서브쿼리가 어떤 rows를 포함한다면 `true` 반환
  * `IN` - 피연산자가 리스트의 어느 한 요소와 일치한다면 `true` 반환
  * `LIKE` - 피연산자가 패턴과 매칭된다면 `true` 반환
  * `NOT` - Boolean 연산자의 결과를 반전
  * `OR` - 어느 한 표현식이 `true` 라면 `true` 반환
  * `SOME` - 하나 이상의 표현식이 `true` 라면 `true` 반환



**AND**

* `AND` 연산자는 `SELECT`, `UPDATE`, `DELETE` 등의 SQL 문의 `WEHRE` 절에서 여러개의 조건을 작성하게 해준다.

  ```sql
  expression1 AND expression2
  ```

  * `AND` 연산자는 모든 표현식이 `true` 로 평가될 때 `true` 를 반환한다.

* 아래 예시는 임금이 5000보다 높고 7000보다 작은 고용인들을 추출하는 것이다.

  ```sql
  SELECT ...
  FROM emplyees
  WHERE
  		salary > 5000 AND salary < 7000
  ORDER BY salary
  ```



**OR**

* `AND` 연산자와 비슷하게, `OR` 연산자는 `WHERE` 문에서 여러개의 조건을 조합하는 데 사용된다.

  ```sql
  expression1 OR expression2
  ```

  * 그러나, `OR` 연산자는 적어도 하나의 평가식만 `true` 로 평가되어 `true` 를 반환한다.

* 예를 들어, 아래 문은 임금이 7000이나 8000인 고용인들을 추출한다.

  ```sql
  SELECT ...
  FROM emplyees
  WHERE
  		salary = 7000 OR salary = 8000
  ORDER BY salary;
  ```

  

**IS NULL**

* `IS NULL` 연산자는 값이 `null` 인지를 판별한다.

* 아래 예시는 핸드폰 번호가 없는 모든 고용인들을 추출한다.

  ```sql
  SELECT ...
  FROM employees
  WHERE phone_number IS NULL
  ORDER BY first_name, last_name;
  ```

  

**BETWEEN**

* `BETWEEN` 연산자는 주어진 최소값과 최대값 사이의 값을 가진 요소들을 추출한다.

  * 여기서 작성한 최대, 최소값은 평가 범위에 포함된다.

* 예를 들어, 아래 예시는 임금이 9000과 12000사이인 고용인들을 추출한다.

  ```sql
  SELECT ...
  FROM emplyees
  WHERE
  		salary BETWEEN 9000 AND 12000
  ORDER BY salary;
  ```

  * 여기서 임금이 9000인 사람과 12000인 사람도 목록에 포함된다.



**IN**

* `IN` 연산자는 특정 값들의 리스트와 값을 비교한다.

  * `IN` 연산자는 적어도 하나의 리스트 요소 값이 일치한다면 `true` 를 반환한다.
  * 아래 예시는 부서 8이나 9에 일하는 모든 고용인을 추출한다.

  ```sql
  SELECT ...
  FROM employees
  WHERE
  		department_id IN (8, 9)
  ORDER BY department_id;
  ```

  

**LIKE**

* `LIKE` 연산자는 와일드 카드 연산자를 사용해 비슷한 값들을 비교한다.

  * SQL은 두 가지 와일드카드를 `LIKE` 연산자의 접속사로 사용할 수 있게한다.
    * `%` - 0, 1, 2 이상 등의 글자들 (0개부터 여러개의 글자 모두 포함)
    * `_` - 단 하나의 문자
  * 아래 문은 이름의 시작이 `jo` 인 고용인을 추출한다.

  ```sql
  SELECT ...
  FROM employees
  WHERE
  		first_name LIKE 'jo%'
  ORDER BY first_name;
  ```

  * 아래 예시는 이름의 두번째 글자가 `h` 인 사람들을 추출한다.

  ```sql
  SELECT ...
  FROM employees
  WHERE
  		first_name LIKE '_h%'
  ORDER BY first_name;
  ```



**ALL**

* `ALL` 연산자는 다른 결과 셋의 모든 값들과 비교한다.

  * `ALL` 연산자 앞에는 비교 연산자가 있어야 하고 서브 쿼리가 뒤따라와야 한다.

  ```sql
  comparison_operator ALL (subquery)
  ```

  * 아래 예시는 부서 8에 있는 모든 고용인의 임금보다 높은 임금을 가진 고용인을 추출한다

  ```sql
  SELECT ...
  FROM employees
  WHERE
  		salary >= ALL (SELECT
                    	salary
                   	FROM
                    	employees
                    WHERE
                    	department_id = 8)
  ORDER BY salary DESC;
  ```



**ANY**

* `ANY` 연산자는 아래와 같이 셋에서 조건에 맞는 값이 있는지를 비교한다.

  ```sql
  comparison_operator ANY(subquery)
  ```

  * `ALL` 연산자와 비슷하게, `ANY` 연산자도 반드시 비교 연산자가 선행되며 서브쿼리가 후행돼야 한다.

* 예를 들어, 아래 문은 모든 부서의 임금 평균보다 높은 임금의 고용자를 뽑는 것이다.

  ```sql
  SELECT
  		...
  FROM
  		employees
  WHERE
  		salary > ANY(SELECT
                  AVG(salary)
                  FROM
                  	employees
                 	GROUP BY department_id)
  ORDER BY first_name, last_name;
  ```

  * `SOME` 은 `ANY` 의 별칭이므로, 이를 서로 교환하여 사용할 수 있다.



#### EXISTS

* `EXISTS` 연산자는 서브쿼리가 어떤 rows 들을 포함하는지 테스트한다.

  ```sql
  EXISTS (subquery)
  ```

  * 만일 서브쿼리가 하나 이상의 row를 반환한다면, `EXISTS` 결과는 참이다.

* 예를 들어, 아래 문은 dependent 가 있는 고용인들을 추출한다.

  ```sql
  SELECT
  		first_name, last_name
  FROM
  		employees e
  WHERE
  		EXISTS(SELECT
            1
            FROM
            		dependents d
            WHERE
            		d.employee_id = e.employee_id)
  ```



여기까지 대략적으로 SQL 논리 연산자들에 대해 알아봤다. 앞으로 하나씩 살펴볼 것이다.



### AND

