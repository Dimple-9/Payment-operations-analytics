# SQL Analysis – Payment Transaction Insights
This project used SQL queries to analyze transaction performance, identify failure trends, and evaluate settlement timelines.

## Transaction Success Rate
Select 
    COUNT(*) AS total_transactions,
    SUM(CASE WHEN status = 'Success' THEN 1 ELSE 0 END) AS successful_transactions,
    ROUND(100.0 * SUM(CASE WHEN status = 'Success' THEN 1 ELSE 0 END) / COUNT(*), 2) AS success_rate
FROM transactions;

## Failure Reason Analysis
Select 
    failure_reason,
    COUNT(*) AS failure_count
FROM transactions
WHERE status = 'Failed'
GROUP BY failure_reason
ORDER BY failure_count DESC;

## Gateway Performance Comparison
Select 
    gateway,
    COUNT(*) AS total_transactions,
    SUM(CASE WHEN status = 'Failed' THEN 1 ELSE 0 END) AS failed_transactions
FROM transactions
GROUP BY gateway;

## Settlement Timeline Monitoring
Select 
    settlement_days,
    COUNT(*) AS transactions
FROM transactions
GROUP BY settlement_days
ORDER BY settlement_days;

## Reconciliation Exceptions
Select 
    transaction_id,
    gateway,
    amount
FROM transactions
WHERE reconciled = 'No';
