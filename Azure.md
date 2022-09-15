# Azure KB

A quick reminder of all relevant Azure things, focused on Data Engineering

# Table of Contents 
1.  [ SQL Pool ](#sql)

<a name="sql"></a>
# 1. SQL Pool

### **Query execution plans**

In Synapse Analytics you can display the query execution plan for a dedicated sql pool at the control and compute node levels using the database consistency check, DBCC PDW_SHOWEXECUTIONPLAN

Note: This process is not supported by serverless SQL pool in Azure Synapse Analytics.

In order to see what is running on an Azure Synapse dedicated pool we can use the following query:

``` sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status], [distribution_id]  
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
order by request_id, [dms_step_index];  
```

Once you have identified a node that you want to analyze, then you can use the DBCC PDW_SHOWEXECUTIONPLAN command to look at the execution plan on a specific distribution and its specific session as shown in the example below:

``` sql
DBCC PDW_SHOWEXECUTIONPLAN ( 1, 375 );
```
