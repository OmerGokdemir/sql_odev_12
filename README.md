# sql_odev_12
SQL 12. Ödevi

## Aşağıdaki sorgu senaryolarını *dvdrental* örnek veri tabanı üzerinden gerçekleştiriniz.


1. *film* tablosunda film uzunluğu *length* sütununda gösterilmektedir. Uzunluğu ortalama film uzunluğundan fazla kaç tane film vardır?

```SQL
      SELECT COUNT(length) FROM film
      WHERE length >
      (
        SELECT AVG(length) FROM film
      );
```

2. *film* tablosunda en yüksek *rental_rate* değerine sahip kaç tane film vardır?

```SQL
      SELECT COUNT(rental_rate) FROM film
      WHERE rental_rate =
      (
        SELECT MAX(rental_rate) FROM film
      )
```

3. *film* tablosunda en düşük *rental_rate* ve en düşük *replacement_cost* değerlerine sahip filmleri sıralayınız.

```SQL
      SELECT title, rental_rate,replacement_cost
      FROM film
      WHERE (rental_rate =
      (
        SELECT MIN(rental_rate) FROM film
      )
        )
      AND
      (replacement_cost =
      (
        SELECT MIN(replacement_cost) FROM film
      )
      )
      ORDER BY title ASC;
```

4. *payment* tablosunda en fazla sayıda alışveriş yapan müşterileri(*customer*) sıralayınız.

```SQL
      SELECT DISTINCT customer.first_name, customer.last_name, payment.customer_id, COUNT(payment.customer_id) AS alisveris_sayisi
      FROM customer LEFT JOIN payment ON customer.customer_id = payment.customer_id
      GROUP BY customer.first_name, customer.last_name, payment.customer_id
      ORDER BY alisveris_sayisi DESC;
```
