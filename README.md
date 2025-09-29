# MOT test for motorcycles
MOT Test is annual test of vehicle safety, roadworthiness aspects and exhaust emissions required in the United Kingdom for most vehicles over three years old. The goal of my project is to analyze results of MOT test committed by Class II, that is all motorcycles with or without sidecars. Class II includes Class I(motos up to 200cc). Period of analysis is 2024.

## Overview of tables
### 'test_result' table
Contains details of individual MOT tests and of the vehicle tested. All tests which could result in a valid pass result are included. 
Column Name  | Description | Notes
--- | --- | ---
**test_id** | Unique identifier for a test | 
**vehicle_id** | Unique id of vehicle | 
**test_date** | Date of test | Will be dropped
**test_class_id** | Id of vehicle class | Will be dropped as we analyze only Class II
**test_type** | Test type | 'NT' (Full initial test),  'RT' (Full retest of vehicle. Derived by system, not selected by NT)
**test_result** | Result of the test | Detailed description in a separate table below
**test_mileage** | Mileage recorded at point of test | 
**postcode_area** | Test location | High-level postcode region
**make** | Vehicle brand | 
**model** | Vehicle model | 
**colour** | Vehicle colour  | Will be dropped
**fuel_type** | Vehicle fuel type | Will be dropped (99.8% motorcycles use petrol)
**cylinder_capacity** | Vehicle engine power | 
**first_use_date** | Vehicle date of first use | 
**completed_date** | Date and time of test completion | 

#### `test_result` column 
| Result Code | Result | Notes |
| :--- | :--- | :--- |
| P | Pass | Test Pass |
| F | Fail | Test Fail |
| PRS | Pass with Rectification at Station | The process where defects may be rectified within one hour after the test, but before recording the result on the Vehicle Test Station (VTS) Device (Vehicle begins the test in a fail condition, but is in pass condition when result is input). |
| ABA | Abandon | The term used when a test cannot be completed because the NT considers it unsafe to continue or because it becomes apparent during the test that certain items cannot be satisfactorily inspected. An appropriate fee may be charged for the test. |
| ABR | Abort | The term used when a test cannot be completed because of a problem with the testing equipment or the NT. No fee may be charged for the test. |

<br>

### 'test_item' table 
Contains details of individual MOT test failure items. 
| Column Name | Description | Notes |
| :--- | :--- | :--- |
| **test_id** | Unique Identifier for a test. References associated test in Vehicle Test Result table. |
| **rfr_id** | Reason for Rejection ID | |
| **rfr_type** | Reason for Rejection Type (detailed description in a separate table below) | 'F', 'P', 'A', 'M' |
| **mot_test_rfr_location_type_id** | Failure Location ID. References associated failure location in Failure Location table. The location ID identifies the lateral, longitudinal and vertical position of the RfR (where applicable). |
| **dangerous_mark** | Dangerous Item Marker | Up to 19ᵗʰ May 2018, where a tester could choose to denote that a failure item was dangerous (will be dropped) |
completed_date | Date and time of test completion | 

#### `rfr_type` column
| Type Code | RfR Type | Notes |
| :--- | :--- | :--- |
| F | Fail | A test failure item. |
| P | PRS | An item in a failing state at the point of test, repaired within one hour of the test and before the result was entered. |
| A | Advisory | An advisory item. |
| M | Minor defect | Minor defect |

<br>

### 'item_detail' table
Contains details of individual RfRs
| Column Name | Description | Notes |
| :--- | :--- | :--- |
| **rfr_id** | Reason for Rejection ID |  
| **test_class_id** | Class of Vehicle Tested | Will be dropped as we analyze only Class II
| **test_item_id** | Test Item ID | References parent test item in Test Item Group table (with Test Class ID) |
| **rfr\_deficiency\_category** | EU category | 'Pre-EU Directive', 'Minor', 'Major', 'Dangerous' |
| **minor_item** | Minor Item Marker – Specifies whether an item can be classified as minor (qualifies for free partial retest). | 
| **rfr_desc** | RfR Short Description | Text printed on VT30 test failure document (Will be dropped ) | 
| **rfr_loc_marker** | RfR Location Marker – Specifies whether further location details are required against this item. | 
| **rfr_insp_manual_desc** | RfR Inspection Manual Description | will be renamed to `rfr_desc`
| **rfr_advisory_text** | Advisory Notice Text | Text printed for type 'A' Test Items on Advisory Notice (Will be dropped ) |
| **test_item_set_section_id** | | References top level test item in Test Item Group table (with Test Class ID) |

<br>

### 'item_group' table 
Contains details of RfR groupings within the test item hierarchy. The top level group for a Test Class is always ‘Vehicle’, with a Test Item ID of 0. 
| Column Name | Description | Notes |
| :--- | :--- | :--- |
| **test\_item\_id** | Test Item ID | Primary Key |
| **test\_class\_id** | Class of Vehicle Tested | Primary Key |
| **parent\_id** | Parent ID | References parent Test Item ID in hierarchy (with Test Class ID) |
| **test\_item\_set\_section\_id** | | References top level test item in hierarchy (with Test Class ID) |
| **item\_name** | Test Item Name | |

<br>

### 'rfr_location' table
Reference for Location IDs in Test Item Table
| Column Name | Description | Notes |
| :--- | :--- | :--- |
| **id** | Failure Location ID | 
| **lateral** | Lateral Location |Boolean value |
| **vertical** | Vertical Location |Boolean value |
| **longitudinal** | Longitudinal Location | Boolean value|


