# Домашнее задание к занятию «`SQL. Часть 2`» - `Барановский Станислав`

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

---

Задание можно выполнить как в любом IDE, так и в командной строке.

## Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.
```sql
select concat(sta.last_name, ' ', sta.first_name) as ФИО_сотрудника_магазина, ci.city as Город_нахождения_магазина, count(cu.store_id) as Количество_пользователей_магазина
from customer cu
join store sto on sto.store_id = cu.store_id
join staff sta on sta.store_id = sto.store_id
join address a on a.address_id = sto.address_id
join city ci on a.city_id = ci.city_id
group by cu.store_id, sta.staff_id, a.address_id, ci.city_id
having count(cu.store_id) > 300;
```
![Скриншот выполнения запроса](https://github.com/StanislavBaranovskii/12-4-hw/blob/main/img/12-4-1.png "Скриншот выполнения запроса")

---
## Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.
```sql
select count(film_id)
from film
where length > (select avg(length) from film);
```
![Скриншот выполнения запроса](https://github.com/StanislavBaranovskii/12-4-hw/blob/main/img/12-4-2.png "Скриншот выполнения запроса")

---
## Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.
```sql
select month(payment_date) as Месяц, count(payment_id) as Количество_аренд
from payment
where month(payment_date) = (select month(payment_date) from payment group by month(payment_date) order by sum(amount) desc limit 1)
group by month(payment_date);
```
![Скриншот выполнения запроса](https://github.com/StanislavBaranovskii/12-4-hw/blob/main/img/12-4-3.png "Скриншот выполнения запроса")

---
## Задание 4*

Посчитайте количество продаж, выполненных каждым продавцом. Добавьте вычисляемую колонку «Премия». Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».
```sql

```
![Скриншот выполнения запроса](https://github.com/StanislavBaranovskii/12-4-hw/blob/main/img/12-4-4.png "Скриншот выполнения запроса")

---
## Задание 5*

Найдите фильмы, которые ни разу не брали в аренду.
```sql

```
![Скриншот выполнения запроса](https://github.com/StanislavBaranovskii/12-4-hw/blob/main/img/12-4-5.png "Скриншот выполнения запроса")

---