---
created: 2025-11-16T08:27
updated: 2025-11-16T08:29
tags:
  - sql
  - gbq
---
changes to a table
  handig: je kan changes op elke tabel ophalen uit GBQ met behulp van
   `FOR SYSTEM TIME AS OF`
  Zo ben je niet afhankelijk van een kolom in de tabel die dit aangeeft of historized tabellen. Ook kan je specifiek de kolommen checken waar je in geinteresseerd bent. 
  
  ### example
  Dit haalt de changes op sinds gisteren voor specifieke kolommen in dim customer bijvoorbeeld;
  
  ```sql
  CREATE TEMP TABLE current_state as
  select UniqueCustomerNumber, CustomerSalesBusinessUnit, CustomerPriority, Segment, Industry from `kramp-sharedmasterdata-prd.kramp_sharedmasterdata_presentation.PRES__DIM__customer__current`
  FOR SYSTEM TIME AS OF CURRENT_TIMESTAMP();
  
  WITH yesterday_state as (select UniqueCustomerNumber, CustomerSalesBusinessUnit, CustomerPriority, Segment, Industry from `kramp-sharedmasterdata-prd.kramp_sharedmasterdata_presentation.PRES__DIM__customer__current`
  FOR SYSTEM TIME AS OF TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 DAY)
  )
  SELECT * FROM current_state
  EXCEPT DISTINCT
  SELECT * FROM yesterday_state
  ```

  de create temp table is nodig omdat je niet 2x dezelfde tabel mag querien met verschillende system time as waardes…