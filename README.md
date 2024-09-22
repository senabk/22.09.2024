SELECT 
    p.ProductID,
    p.ProductName,
    YEAR(s.SaleDate) AS SaleYear,
    SUM(s.Quantity * p.Price) AS TotalSalesAmount,
    SUM(s.Quantity) AS NumberOfSales
FROM 
    Products p
JOIN 
    Sales s ON p.ProductID = s.ProductID
GROUP BY 
    p.ProductID, 
    p.ProductName, 
    YEAR(s.SaleDate)
ORDER BY 
    SaleYear, 
    p.ProductID;
WITH TotalSales AS (
    SELECT 
        p.ProductID,
        p.ProductName,
        SUM(s.Quantity * p.Price) AS TotalSalesAmount
    FROM 
        Products p
    JOIN 
        Sales s ON p.ProductID = s.ProductID
    GROUP BY 
        p.ProductID, 
        p.ProductName
)

SELECT 
    ProductID,
    ProductName,
    TotalSalesAmount
FROM 
    TotalSales
ORDER BY 
    TotalSalesAmount DESC
LIMIT 1;
