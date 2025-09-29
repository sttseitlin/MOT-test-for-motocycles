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
test_type | Two types of test: NT - full initial test, RT - full retest of vehicle

