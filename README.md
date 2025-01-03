# NSEstocks-project

CREATE TABLE stock_summaryNSE 
(
   stock_symbol VARCHAR(10),
   `date` DATE,
   open_price FLOAT,
   high_price FLOAT,
   low_price FLOAT,
   prev_close FLOAT,
   ltp FLOAT,    -- ltp : LAST TRADED PRICE
   indicative_close FLOAT,
   `change` FLOAT,
   percentage_change FLOAT,
   volume INT,
   value_crores FLOAT,
   fifty_two_week_high FLOAT,
   fifty_two_week_low FLOAT,
   thirty_day_change FLOAT
);

INSERT INTO stock_summaryNSE
(
   stock_symbol, `date`, open_price, high_price, low_price, prev_close, ltp,indicative_close, `change`, percentage_change, volume, value_crores,fifty_two_week_high,fifty_two_week_low, thirty_day_change
)
VALUES
('TATAMOTORS', '2025-01-03', '768.00', '785.70',	'761.45',	'765.05',	'785.30',	'NULL',	'20.25',	'2.65',	'7950714',	'614.65',	'1179.00',	'717.70',	'-4.52'),
('TITAN', '2025-01-03', '3395.00',	'3478.15',	'3377.95',	'3388.95',	'3472.10',	'NULL',	'83.15',	'2.45',	'559014',	'192.49',	'3886.95',	'3055.65',	'1.69');

SELECT * FROM stock_summaryNSE;
SELECT stock_symbol, date, open_price, high_price, low_price, prev_close, ltp, change, percentage_change
FROM stock_summary
WHERE change > 0;

SELECT stock_symbol, date, volume
FROM stock_summaryNSE
ORDER BY volume DESC
LIMIT 3;

Fetch stocks whose current price is within 5% of their 52-week high:

SELECT stock_symbol, ltp, fifty_two_week_high, 
       ((fifty_two_week_high - ltp) / fifty_two_week_high * 100) AS proximity_to_high
FROM stock_summary
WHERE ltp >= fifty_two_week_high * 0.95;

Retrieve stocks with high trading activity (e.g., volume > 1 million and value > 500 crores):
SELECT stock_symbol, date, volume, value_crores
FROM stock_summaryNSE
WHERE volume > 1000000 AND value_crores > 500;
   
SELECT stock_symbol, date, thirty_day_change
FROM stock_summaryNSE
WHERE stock_symbol = 'TATAMOTORS';
WHERE stock_symbol = 'TITAN';

Calculate 30-Day Change Percentage for a Specific Stock:
SELECT stock_symbol, date, thirty_day_change
FROM stock_summaryNSE
WHERE stock_symbol = 'TATAMOTORS','TITAN;

Fetch the last 30 days of data for a specific stock:

SELECT stock_symbol, date, open_price, high_price, low_price, ltp, percentage_change
FROM stock_summaryNSE
WHERE stock_symbol = 'TITAN'
ORDER BY date DESC
LIMIT 30;

Identify stocks likely to break their 52-week high based on their recent trends:

SELECT stock_symbol, ltp, fifty_two_week_high, 
       ((ltp / fifty_two_week_high) * 100) AS percentage_to_high
FROM stock_summary
WHERE percentage_to_high >= 95
ORDER BY percentage_to_high DESC;


import java.sql.*;

public class StockQuery {
    public static void main(String[] args) {
        String dbUrl = "jdbc:mysql://localhost:3306/stock_db";
        String username = "NUTHANAPATI HEMALATHA";
        String password = "FGH123456789";
        String query = "SELECT stock_symbol, ltp, fifty_two_week_high FROM stock_summary WHERE ltp >= fifty_two_week_high * 0.95";
        try (Connection connection = DriverManager.getConnection(dbUrl, username, password);
             Statement statement = connection.createStatement();
             ResultSet resultSet = statement.executeQuery(query)) {
            while (resultSet.next()) {
                String stockSymbol = resultSet.getString("stock_symbol");
                float ltp = resultSet.getFloat("ltp");
                float fiftyTwoWeekHigh = resultSet.getFloat("fifty_two_week_high");
                System.out.print("Stock: %s, LTP: %.2f, 52W High: %.2f%n", stockSymbol, ltp, fiftyTwoWeekHigh);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}

