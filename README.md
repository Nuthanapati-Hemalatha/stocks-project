# NSEstocks-project

CREATE TABLE stock_summaryNSE 
(
   stock_symbol VARCHAR(10),
   data DATE,
   open_price FLOAT,
   high_price FLOAT,
   low_price FLOAT,
   prev_close FLOAT,
   ltp FLOAT,    -- ltp : LAST TRADED PRICE
   indicative_close FLOAT,
   change FLOAT,
   percentage_change FLOAT,
   volume INT,
   value_crores FLOAT,
   fifty_two_week_high FLOAT,
   fifty_two_week_low FLOAT,
   thirty_day_change FLOAT,
);

INSERT INTO stock_summaryNSE
(
   stock_symbol, date, open_price, high_price, low_price, prev_close, ltp,indicative_close, change, percentage_change, volume, value_crores,fifty_two_week_high,fifty_two_week_low, thirty_day_change
)
VALUES
('TATAMOTORS', '2025-01-03', '768.00', '785.70',	'761.45',	'765.05',	'785.30',	'-',	'20.25',	'2.65',	'79,50,714',	'614.65',	'1,179.00',	'717.70',	'-4.52'),
('TITAN', '2025-01-03', '3,395.00',	'3,478.15',	'3,377.95',	'3,388.95',	'3,472.10',	'-',	'83.15',	'2.45',	'5,59,014',	'192.49',	'3,886.95',	'3,055.65',	'1.69'),

SELECT * FROM stock_summaryNSE;
SELECT stock_symbol, date, open_price, high_price, low_price, prev_close, ltp, change, percentage_change
FROM stock_summary
WHERE change > 0;

SELECT stock_symbol, date, volume
FROM stock_summaryNSE
ORDER BY volume DESC
LIMIT 3;
   
