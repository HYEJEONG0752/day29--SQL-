# Day 2: 고급 SQL 쿼리 과제

### **1. INNER JOIN 문제**

**설명**: 여러 테이블을 조인하여 관련 데이터를 함께 가져오는 방법을 연습합니다.

**문제**:

다음의 테이블들이 있습니다:

- `students` (student_id, name)
- `enrollments` (student_id, course_id)
- `courses` (course_id, course_name)

각 학생이 수강 중인 과목의 이름을 모두 출력하는 쿼리를 작성하세요.
```sql
    SELECT s.name AS student_name, c.course_name
    FROM students s
    INNER JOIN enrollments e ON s.student_id = e.student_id
    INNER JOIN courses c ON e.course_id = c.course_id;
```
---

### **2. LEFT JOIN 문제**

**설명**: 왼쪽 테이블의 모든 행과 오른쪽 테이블의 일치하는 행을 가져오는 방법을 연습합니다.

**문제**:

다음의 테이블들이 있습니다:

- `employees` (employee_id, name, dept_id)
- `departments` (dept_id, dept_name)

모든 직원의 이름과 그들의 부서 이름을 가져오되, 부서가 없는 직원도 포함하여 부서가 없는 경우 부서 이름을 'None'으로 표시하는 쿼리를 작성하세요.
```sql
SELECT e.name AS employee_name, COALESCE(d.dept_name, 'None') AS department_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.dept_id;
```
---

### **3. RIGHT JOIN 문제**

**설명**: 오른쪽 테이블의 모든 행과 왼쪽 테이블의 일치하는 행을 가져오는 방법을 연습합니다.

**문제**:

다음의 테이블들이 있습니다:

- `products` (product_id, supplier_id, product_name)
- `suppliers` (supplier_id, supplier_name)

모든 공급업체의 이름과 그들이 제공하는 제품의 이름을 가져오되, 제품이 없는 공급업체도 포함하여 제품 이름을 'No Product'로 표시하는 쿼리를 작성하세요.
```sql
SELECT s.supplier_name AS supplier_name, COALESCE(p.product_name, 'No Product') AS product_name
FROM suppliers s
RIGHT JOIN products p ON s.supplier_id = p.supplier_id;
```
---

### **4. FULL OUTER JOIN 문제**

**설명**: 두 테이블의 모든 행을 가져와서 일치하는 데이터를 결합하는 방법을 연습합니다.

**문제**:

다음의 테이블들이 있습니다:

- `students` (student_id, name)
- `clubs` (club_id, club_name)
- `club_memberships` (student_id, club_id)

모든 학생과 모든 동아리를 가져오고, 학생이 어떤 동아리에 소속되어 있다면 그 동아리 이름을, 아니라면 NULL을 표시하는 쿼리를 작성하세요.
```sql
SELECT s.student_id, s.name AS student_name, c.club_id, c.club_name AS club_name
FROM students s
FULL OUTER JOIN club_memberships cm ON s.student_id = cm.student_id
FULL OUTER JOIN club c ON cm.club_id = c.club_id;
```
---

### **5. SELF JOIN 문제**

**설명**: 같은 테이블을 조인하여 계층적 또는 관련 데이터를 비교하는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `employees` (employee_id, name, manager_id)

각 직원의 이름과 그들의 매니저 이름을 함께 출력하는 쿼리를 작성하세요. 매니저가 없는 경우 매니저 이름을 'No Manager'로 표시하세요.
```sql
SELECT e.employee_id, e.name AS employee_name, COALESCE(m.name, 'No Manager') AS Manager_name
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.employee_id;
```
---

### **6. GROUP BY 및 HAVING 문제**

**설명**: 데이터를 그룹화하고 그룹화된 데이터에 조건을 적용하는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `sales` (sale_id, region, amount)

각 지역별 총 판매액을 계산하고, 총 판매액이 100,000 이상인 지역만 지역 이름과 총 판매액을 출력하는 쿼리를 작성하세요.
```sql
SELECT region, SUM(amount) AS total_sales
FROM sales
GROUP BY region
HAVING SUM(amount) >= 100000;
```
---

### **7. ORDER BY 및 LIMIT 문제**

**설명**: 데이터를 정렬하고 결과 수를 제한하는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `products` (product_id, product_name, price)

가격이 가장 비싼 상위 5개의 제품 이름과 가격을 출력하는 쿼리를 작성하세요.
```sql
SELECT product_name, price
FROM products
ORDER BY price DESC
LIMIT 5;
```
---

### **8. COUNT 함수 문제**

**설명**: 특정 조건에 맞는 행의 개수를 세는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `orders` (order_id, customer_id, order_date)

각 고객별 주문 횟수를 계산하고, 주문 횟수가 5회 이상인 고객의 ID와 주문 횟수를 출력하는 쿼리를 작성하세요.
```sql
SELECT customer_id, COUNT(order_id) AS order_count
FROM orders
GROUP BY customer_id
HAVING COUNT(order_id) >= 5;    -- 주문 횟수가 5회이상인 고객만 결과에 포함되도록 필터링
```
---

### **9. SUM 및 AVG 함수 문제**

**설명**: 합계와 평균을 계산하는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `employees` (employee_id, name, department, salary)

각 부서별 총 급여 합계와 평균 급여를 계산하고 부서 이름, 총 합계, 평균 급여를 출력하는 쿼리를 작성하세요.
```sql
SELECT department, SUM(salary) AS total_salary, AVG(salary) AS average_salary
FROM employees
GROUP BY department;
```
---

### **10. MAX 및 MIN 함수 문제**

**설명**: 최대값과 최소값을 찾는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `products` (product_id, product_name, price)

전체 제품 중 가장 비싼 제품과 가장 저렴한 제품의 이름과 가격을 각각 출력하는 쿼리를 작성하세요.
```sql
-- 가장 비싼 제품
SELECT product_name, price
FROM products
WHERE price = (SELECT MAX(price) FROM products);

-- 가장 저렴한 제품
SELECT product_name, price
FROM products
WHERE price = (SELECT MIN(price) FROM products);

-- 단일 쿼리 ('UNION'사용)
SELECT product_name, price, 'Most Expensive' AS Product_type
FROM products
WHERE price = (
    SELECT MAX(price) FROM products)

UNION ALL

SELECT product_name, price, 'Least Expensive' AS Product_type
FROM products
WHERE price = (
    SELECT MIN(price)
    FROM products
);

```
---

### **11. 서브쿼리 문제**

**설명**: 서브쿼리를 사용하여 복잡한 조건을 적용하는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `employees` (employee_id, name, salary)

직원들의 평균 급여보다 높은 급여를 받는 직원의 이름과 급여를 출력하는 쿼리를 작성하세요.
```SQL
SELECT name, salary
FROM employees
WHERE salary > (    -- 직원의 급여가 특정 조건을 만족하는지 확인
    SELECT AVG(salary) 
    FROM employees
);
```
---

### **12. EXISTS 서브쿼리 문제**

**설명**: `EXISTS`를 사용하여 데이터의 존재 여부를 확인하는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `customers` (customer_id, name)
- `orders` (order_id, customer_id, order_date)

주문을 한 적이 있는 고객의 이름과 ID를 출력하는 쿼리를 작성하세요.
```sql
SELECT customer_id, name
FROM customers c
WHERE EXISTS (  -- 'EXISTS'키워드를 사용하여 서브쿼리의 결과가 존재하는지 확인
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```
---

### **13. UNION 문제**

**설명**: 여러 쿼리의 결과를 결합하여 하나의 결과로 만드는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `current_students` (student_id, name)
- `alumni` (alumni_id, name)

현재 재학생과 졸업생의 이름을 모두 포함하는 명단을 중복 없이 출력하는 쿼리를 작성하세요.
```sql
SELECT name
FROM current_students

UNION   -- 첫번째 쿼리의 결과와 두번째 쿼리의 결과를 결합.중복된 이름은 자동으로 제거

SELECT name
FROM alumni;
```
---

### **14. INTERSECT 문제**

**설명**: 여러 쿼리의 공통 결과를 추출하는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `customers` (customer_id, name)
- `subscribers` (customer_id, email)

회원이면서 뉴스레터 구독자인 고객의 이름을 출력하는 쿼리를 작성하세요.
```sql
SELECT name
FROM customers

INTERSECT   -- 첫번재 쿼리의 결과와 두번째 쿼리의 결과의 교집합

SELECT c.name
FROM customers c
JOIN subscribers s ON c.customer_id = s.customer_id;
```
---

### **15. EXCEPT 문제**

**설명**: 한 쿼리 결과에서 다른 쿼리 결과를 제외하는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `students` (student_id, name)
- `graduates` (student_id, graduation_date)

졸업하지 않은 학생들의 이름을 출력하는 쿼리를 작성하세요.
```sql
SELECT name
FROM students

EXCEPT  -- 첫번쨰 쿼리의 결과에서 두번째 쿼리의 결과 제외

SELECT s.name
FROM students s
JOIN graduates g ON s.student_id = g.student_id;
```
---

### **16. 공통 테이블 표현식 (CTE) 문제**

**설명**: CTE를 사용하여 복잡한 쿼리를 가독성 있게 작성하는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `employees` (employee_id, name, department, salary)

CTE를 사용하여 각 부서별 평균 급여를 계산하고, 평균 급여보다 낮은 급여를 받는 직원의 이름, 부서, 급여를 출력하는 쿼리를 작성하세요.
```sql
WITH departmentAverage AS (
    -- 각 부서별 평균 급여 계산
    SELECT department, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department
)
-- 평균 급여보다 낮은 급여를 받는 직원 선택
SELECT e.name, e.department, e.salary
FROM employees e
JOIN departmentAverage da ON e.department = da.department
WHERE e.salary < da.avg_salary  -- 평균 급여보다 낮은 직원 필터링
ORDER BY e.department, e.salary;    -- 부서와 급여로 정렬
```
---

### **17. 재귀 CTE 문제**

**설명**: 재귀 CTE를 사용하여 계층적 데이터를 처리하는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `categories` (category_id, category_name, parent_id)

재귀 CTE를 사용하여 모든 카테고리와 하위 카테고리를 계층적으로 표시하는 쿼리를 작성하세요.
```sql
WITH RECURSIVE categoriesHierachy AS (
    SELECT category_id, category_name, parent_id, 0 AS level
    FROM categories
    WHERE parent_id IS NULL

    UNION ALL

    SELECT c.category_id, c.category_name, c.parent_id, ch.level + 1
    FROM categories
    INNER JOIN categoriesHierachy ch ON c.parent_id = ch.category_id
)

SELECT category_id, category_name, parent_id, level
FROM categoriesHierachy
ORDER BY level, category_id;
```
---

### **18. 윈도우 함수 문제**

**설명**: 윈도우 함수를 사용하여 집계와 순위를 계산하는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `sales` (sale_id, salesperson_id, amount, sale_date)

각 영업사원의 총 판매액과 전체 영업사원 중에서의 판매액 순위를 계산하여 영업사원 ID, 총 판매액, 순위를 출력하는 쿼리를 작성하세요.
```sql
SELECT  salesperson_id, SUM(amount) AS total_sales, RANK() OVER (ORDER BY SUM(amount) DESC) AS sales_rank
FROM sales
GROUP BY salesperson_id
ORDER BY sales_rank;
```
---

### **19. 트랜잭션 문제**

**설명**: 트랜잭션을 사용하여 데이터 일관성을 유지하는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `accounts` (account_id, customer_id, balance)

계좌 ID가 1인 계좌에서 계좌 ID가 2인 계좌로 500달러를 이체하는 트랜잭션을 작성하세요. 이체 중 오류가 발생하면 모든 작업이 취소되도록 해야 합니다.
```sql
BEGIN;
UPDATE accounts
SET balance = balance - 500
WHERE account_id = 1;
IF ( SELECT balance FROM accounts WHERE account_id = 1) < 0 THEN 
ROLLBACK;
ELSE UPDATE accounts SET balance = balance + 500
WHERE account_id = 2;
COMMIT;
END IF;
```
---

### **20. 인덱스 및 성능 문제**

**설명**: 인덱스를 생성하여 쿼리 성능을 향상시키는 방법을 연습합니다.

**문제**:

다음의 테이블이 있습니다:

- `employees` (employee_id, name, department, hire_date)

`department`와 `hire_date` 컬럼에 복합 인덱스를 생성하는 쿼리를 작성하고, 특정 부서에서 최근에 고용된 직원 10명의 이름과 고용일을 빠르게 조회하는 쿼리를 작성하세요.
```sql
-- 복합 인덱스 생성
CREATE INDEX idx_department_hire_date ON employees(department, hire_date);

-- 특정부서에서 최근에 고용된 직원 10명 조회
SELECT name, hire_date
FROM employees
WHERE department = '특정부서명'
ORDER BY hire_date DESC
LIMIT 10;
```