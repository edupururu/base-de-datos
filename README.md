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
