# base-de-datos
-- 1) Genere un reporte mostrando el nombre y apellido de cada customer con la cantidad 
	-- de películas que alquilo y la cantidad de dinero que ha gastado.
	-- La cantidad de películas debe ser el total (incluyendo las que no ha devuelto todavía)
	-- mostrar solo los clientes que hayan gastado entre 100 y 150 dolares.
	
SELECT customer.first_name, customer.last_name, COUNT(rental.rental_id), SUM(payment.amount)
  FROM customer 
    INNER JOIN rental USING (customer_id)
    INNER JOIN inventory USING (inventory_id)
    INNER JOIN payment USING(rental_id)
	GROUP BY customer.first_name, customer.last_name having SUM(payment.amount) > 100 and SUM(payment.amount) <150
	order by SUM(payment.amount) ;


Muestre un reporte de la cantidad de películas rentadas por país y por categoría de películas
Columnas a mostrar nombre del país, nombre la categoría y cantidad de películas alquiladas
Ejemplo:
Pais Categoria Cantidad
Argentina Action 25
Argentina Animation 26
Argentina Children 13
Argentina Classics 18
(CAMBIEN TODO... CAMBIEN COMO LLEGO HASTA AHI)

SELECT c.country, ci.name, SUM(r.rental_id)
FROM category ci
INNER JOIN film_category USING(category_id)
INNER JOIN film USING(film_id)
INNER JOIN inventory USING(film_id)
INNER JOIN rental r USING(inventory_id)
INNER JOIN customer USING(customer_id)
INNER JOIN address USING(address_id)
INNER JOIN city USING(city_id)
INNER JOIN country c USING(country_id)
GROUP BY c.country, ci.category_id
HAVING SUM(r.rental_id);
