# MOT test for motorcycles
MOT Test is annual test of vehicle safety, roadworthiness aspects and exhaust emissions required in the United Kingdom for most vehicles over three years old. The goal of my project is to analyze results of MOT test committed by Class II, that is all motorcycles with or without sidecars. Class II includes Class I(motos up to 200cc). Period of analysis is 2024.

## Overview of tables
### mt (original name: test_result)

Column name  | Description
--- | ---
test_id | Unique id of test, each separate test has own id
vehicle_id | Unique id of vehicle
test_date | Date of test
test_class_id | Id of vehicle class(will be dropped as we analyze only Class II)
test_type | Test type
test_result | Result of the test
test_mileage | Mileage recorded at point of test
postcode_area | Test location (high-level postcode region) 
make | Vehicle brand
model | Vehicle model
colour | Vehicle colour (will be dropped)
fuel_type | Vehicle fuel type (will be dropped)
cylinder_capacity | Vehicle engine power
first_use_date | Vehicle date of first use
completed_date | Date and time of test completion

# test_result column 
| Result Code | Result | Notes |
| :--- | :--- | :--- |
| P | Pass | Test Pass |
| F | Fail | Test Fail |
| PRS | Pass with Rectification at Station | The process where defects may be rectified within one hour after the test, but before recording the result on the Vehicle Test Station (VTS) Device (Vehicle begins the test in a fail condition, but is in pass condition when result is input). |
| ABA | Abandon | The term used when a test cannot be completed because the NT considers it unsafe to continue or because it becomes apparent during the test that certain items cannot be satisfactorily inspected. An appropriate fee may be charged for the test. |
| ABR | Abort | The term used when a test cannot be completed because of a problem with the testing equipment or the NT. No fee may be charged for the test. |

