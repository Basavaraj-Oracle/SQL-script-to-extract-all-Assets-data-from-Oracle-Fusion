# SQL-script-to-extract-all-Assets-data-from-Oracle-Fusion
SQL script to extract all Assets data from Oracle Fusion


Here is an SQL script to extract all assets data from Oracle Fusion. This script retrieves data from the **Fixed Assets** module. You may need to modify it based on specific requirements, such as custom fields or additional data.

```sql

SELECT 
    faa.asset_number AS "Asset Number",
    faa.asset_name AS "Asset Name",
    faa.asset_category AS "Asset Category",
    faa.book_type_code AS "Book Type",
    faa.date_placed_in_service AS "In Service Date",
    faa.cost AS "Asset Cost",
    faa.ytd_depreciation AS "YTD Depreciation",
    faa.accumulated_depreciation AS "Accumulated Depreciation",
    faa.net_book_value AS "Net Book Value",
    faa.depreciation_method AS "Depreciation Method",
    faa.depreciation_start_date AS "Depreciation Start Date",
    faa.retirement_date AS "Retirement Date",
    faa.asset_status AS "Asset Status",
    fab.location_code AS "Asset Location",
    fab.organization_code AS "Owning Organization"
FROM 
    fa_assets faa
LEFT JOIN 
    fa_book_controls fab ON faa.book_id = fab.book_id
WHERE 
    faa.asset_status IN ('NEW', 'ACTIVE', 'RETIRED')
ORDER BY 
    faa.asset_number;
```

 **Explanation of the Query:**
- **Tables Used:**
  - `fa_assets`: Contains details of assets such as cost, depreciation, and category.
  - `fa_book_controls`: Includes information about asset books and location details.
  
- **Key Columns:**
  - `asset_number`: Unique identifier for each asset.
  - `asset_name`: Name or description of the asset.
  - `asset_category`: The category under which the asset is classified.
  - `book_type_code`: Defines the type of asset book (e.g., Corporate, Tax).
  - `cost`: Original cost of the asset.
  - `ytd_depreciation`: Year-to-date depreciation amount.
  - `accumulated_depreciation`: Total depreciation amount accumulated so far.
  - `net_book_value`: Current value of the asset after depreciation.
  - `location_code`: Location of the asset.
  - `organization_code`: The owning department or organization.

 **Customizations:**
- Add additional joins or columns if you need more specific details like lease information or asset maintenance data.
- Filter results using the `WHERE` clause for specific criteria (e.g., `asset_status`, `asset_category`).

 **Execution Note:**
Ensure you have the appropriate permissions to access the `fa_assets` and `fa_book_controls` tables in Oracle Fusion.
