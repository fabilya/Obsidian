Чаще всего используется, когда нужно построить некую иерархию, когда есть иерархические взаимоотношения между данными

```SQL
CREATE TABLE employee(
	employee_id INT PRIMARY KEY
	first_name VARCHAR (255) NOT NULL,
	last_name VARCHAR (255) NOT NULL,
	manager_id INT,
	FOREIGN KEY (manager_id) REFERENCES employee (employee_id)
);
```
>У каждого работника (необязательно) может быть менеджер, он тоже является обычным работником

Данные в БД:
"employee_id"	"first_name"	"last_name"	"manager_id"
1	"Windy"	"Hays"	
2	"Ava"	"Christensen"	1
3	"Hassan"	"Conner"	1
4	"Anna"	"Reeves"	2
5	"Sau"	"Norman"	2
6	"Kelsie"	"Hays"	3
7	"Tory"	"Goff"	3
8	"Sally"	"Lester"	3
___
Нужно вывести имена и фамилии работников в результирующем наборе, и дополнительно имя его менеджера
```SQL
SELECT e.first_name || ' ' || e.last_name AS employee,
	   m.first_name || ' ' || m.last_name AS manager
FROM employee e -- даем псевдоним "e"
LEFT JOIN employee m ON m.employee_id = e.manager_id
ORDER BY manager
	"Anna Reeves"	"Ava Christensen"
	"Sau Norman"	"Ava Christensen"
	"Sally Lester"	"Hassan Conner"
	"Kelsie Hays"	"Hassan Conner"
	"Tory Goff"	"Hassan Conner"
	"Hassan Conner"	"Windy Hays"
	"Ava Christensen"	"Windy Hays"
	"Windy Hays"	
```

