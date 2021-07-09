SELECT
    product_name,
    coalesce(sum(
            CASE
                WHEN time_paid IS NULL
                AND time_canceled IS NULL THEN line_total_price
                ELSE 0
            END),
        0) AS amount_due,
    coalesce(sum(
            CASE
                WHEN time_paid IS NOT NULL THEN line_total_price
                ELSE 0
            END),
        0) AS amount_paid,
    coalesce(sum(
            CASE
                WHEN time_canceled IS NOT NULL THEN line_total_price
                ELSE 0
            END),
        0) AS amount_canceled,
    coalesce(sum(
            CASE
                WHEN time_paid IS NOT NULL
                AND time_refunded IS NOT NULL THEN line_total_price
                ELSE 0
            END),
        0) AS amount_refunded
FROM
    product prd
    LEFT JOIN invoice_item inv_item ON prd.id = inv_item.product_id
    LEFT JOIN invoice inv ON inv.id = inv_item.invoice_id
GROUP BY
    product_name
ORDER BY
    1;
