# SSIS_project

I designed and developed a real-world SSIS ETL pipeline with the following components.

## Architecture and Flow
Multiple SQL Server source systems  
Centralized data warehouse target  
End-to-end Control Flow and Data Flow design  

## Key ETL Components Used
Lookup (detect new vs changed records)  
Derived Column (data transformation and flags)  
Conditional Split (routing data based on change logic)  
Merge / Merge Join  
Variables and Parameters  
Error handling and rerunnable package design  

## Business Logic Implemented
Slowly Changing Dimension (SCD Type 2) for employee data  
Full history tracking with effective dates  
Ensured only one active record (IsCurrent = 1) per employee  
Handled multiple department changes across different runs  
Prevented duplicate inserts on re-execution (true incremental load)  

## Challenges Solved
Managing multiple updates for the same key  
Ensuring data correctness during package reruns  
Debugging edge cases where history logic failed  
Designing ETL to behave correctly in production-like scenarios, not just first runs  

## IMPORTANT

```yaml
project_tools:
  etl_tool:
    name: SQL Server Integration Services (SSIS)
    purpose: Build, schedule, and manage ETL pipelines for data integration

  source_systems:
    - type: SQL Server
      role: Source
      description: Multiple source databases providing employee and payroll data

  target_system:
    type: SQL Server
    role: Data Warehouse
    description: Centralized warehouse storing current and historical employee records

  ssis_components:
    control_flow:
      - Execute SQL Task:
          description: Prepare staging tables and manage pre/post load operations
      - Sequence Container:
          description: Group ETL steps for logical execution control

    data_flow:
      - OLE DB Source:
          description: Extract data from SQL Server source systems
      - Lookup:
          description: Identify new vs changed records based on business keys
      - Derived Column:
          description: Create calculated columns, flags, and effective dates
      - Conditional Split:
          description: Route rows based on change detection logic
      - Merge:
          description: Combine multiple sorted data streams
      - Merge Join:
          description: Join source data with existing target records
      - OLE DB Destination:
          description: Load transformed data into warehouse tables

  transformations_logic:
    scd_type:
      type: Slowly Changing Dimension Type 2
      description: Maintain full historical tracking of employee changes
    incremental_load:
      description: Load only new or changed records on each execution
    current_record_flag:
      column: IsCurrent
      rule: Ensure only one active record per employee

  package_features:
    variables:
      description: Store runtime values and control package behavior
    parameters:
      description: Enable environment-based configuration
    error_handling:
      description: Capture and handle data and execution errors
    rerunnable_design:
      description: Safe re-execution without duplicate or incorrect data loads

  challenges_handled:
    - Multiple updates for the same business key
    - Correct history maintenance across reruns
    - Prevention of duplicate inserts
    - Production-like data consistency and reliability


Running Windows on Mac was a concern for me, but Parallels Desktop worked incredibly smooth 🚀
I was able to set up Windows quickly and run Visual Studio + SSIS without lag or crashes. Performance felt native, switching between macOS and Windows apps was seamless, and the overall experience was very stable.
If you’re on a Mac and need Windows-only tools, I highly recommend Parallels Desktop.
Download link: https://www.parallels.com/products/desktop/
Hope this helps others facing the same setup challenge
