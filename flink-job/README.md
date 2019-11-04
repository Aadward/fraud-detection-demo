# Dynamic Fraud Detection Demo with Apache Flink

## Introduction


### Instructions:

1. Start `netcat`:
```
nc -lk 9999
```
2. Run main method of `com.dataartisans.dynamicrules.RulesEvaluator`
3. Submit to netcat in correct format:
rule_id, (rule_state), (aggregation keys), (unique keys), (aggregateFieldName field), (aggregation function), (limit operator), (limit), (window size in minutes)

Examples:

1,(active),(paymentType),,(paymentAmount),(SUM),(>),(50),(20)
1,(delete),(paymentType),,(paymentAmount),(SUM),(>),(50),(20)
2,(active),(payeeId),,(paymentAmount),(SUM),(>),(10),(20)
2,(pause),(payeeId),,(paymentAmount),(SUM),(>),(10),(20)

Examples JSON:
{ "ruleId": 1, "ruleState": "ACTIVE", "groupingKeyNames": ["paymentType"], "unique": [], "aggregateFieldName": "paymentAmount", "aggregatorFunctionType": "SUM","limitOperatorType": "GREATER","limit": 500, "windowMinutes": 20}


{"ruleState": "CONTROL", "controlType":"DELETE_RULES_ALL"}
{"ruleState": "CONTROL", "controlType":"EXPORT_RULES_CURRENT"}
{"ruleState": "CONTROL", "controlType":"CLEAR_STATE_ALL"}

1,(active),(paymentType),,(paymentAmount),(SUM),(>),(1000),(20)
2,(active),(payeeId),,(paymentAmount),(SUM),(>),(1000),(20)

CLI params:
--data-source kafka --rules-source kafka --alerts-sink kafka --rules-export-sink kafka

1,(active),(paymentType),,(COUNT_FLINK),(SUM),(>),(50),(20)