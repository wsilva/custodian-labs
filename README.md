# custodian-labs

Repo com testes de estudo do custodian

# Exempo de uso

Depois de logado na AWS

Executrando com dry run - ignora as actions:

```bash
AWS_PROFILE=wsilva \
    custodian run \
        --cache-period 0 \
        --output-dir output \
        --dry-run \
        --verbose \
        cloudwatch-logs-without-rotation.yaml
```

```txt
2024-09-25 18:29:55,179: custodian.cache:DEBUG Disabling cache
2024-09-25 18:29:55,179: custodian.commands:DEBUG Loaded file cloudwatch-logs-without-rotation.yaml. Contains 1 policies
2024-09-25 18:29:55,186: custodian.aws:DEBUG using default region:us-east-1 from boto
2024-09-25 18:29:56,501: custodian.output:DEBUG Storing output with <LogFile file://./log-groups-with-no-rotation/custodian-run.log>
2024-09-25 18:29:56,517: custodian.policy:DEBUG Running policy:log-groups-with-no-rotation resource:aws.log-group region:us-east-1 c7n:0.9.40
2024-09-25 18:29:58,029: custodian.resources.loggroup:DEBUG Using region us-east-1 for resource tagging
2024-09-25 18:29:58,984: custodian.resources.loggroup:DEBUG Filtered from 49 to 49 loggroup
2024-09-25 18:29:58,984: custodian.policy:INFO policy:log-groups-with-no-rotation resource:aws.log-group region:us-east-1 count:49 time:2.47
2024-09-25 18:29:58,985: custodian.output:DEBUG metric:ResourceCount Count:49 policy:log-groups-with-no-rotation restype:aws.log-group scope:policy
2024-09-25 18:29:58,985: custodian.output:DEBUG metric:ApiCalls Count:3 policy:log-groups-with-no-rotation restype:aws.log-group
```

Report

```bash
AWS_PROFILE=wsilva 
    custodian report \
        --output-dir output/ \
        cloudwatch-logs-without-rotation.yaml
```

Saída

```txt
"logGroupName","creationTime"
"/aws-dynamodb/imports","1664391092882"
"/aws-glue/jobs/error","1682703893377"
"/aws-glue/jobs/logs-v2","1682703922417"
"/aws-glue/jobs/output","1682703939357"
"/aws-glue/sessions/error","1691404652210"
"/aws-glue/testconnection/error/rds-shared-mssql-industrial","1691503648296"
"/aws-glue/testconnection/output/rds-shared-mssql-industrial","1691503652346"
"/aws/apigateway/welcome","1636567083337"
...
"/aws/lambda/start-stop-aws-resources","1724498156549"
"/aws/lambda/start-stop-resources","1714039235505"
"API-Gateway-Execution-Logs_00ehz58xi9/hml","1658842018968"
"API-Gateway-Execution-Logs_6sh77itnfd/hml","1667488069222"
"API-Gateway-Execution-Logs_am9fd0d74h/hml","1692386174793"
"API-Gateway-Execution-Logs_ao9f4f5ds6/hml","1636567278057"
"API-Gateway-Execution-Logs_qizv4dapk9/hml","1694719198893"
"API-Gateway-Execution-Logs_qz0jgpmvs9/hml","1664390366564"
"API-Gateway-Execution-Logs_v805t79jw4/hml","1692727582626"
"API-Gateway-Execution-Logs_wisbcy84pa/hml","1717616494326"
"API-Gateway-Execution-Logs_xjex37c5ul/hml","1715285366292"
"RDSOSMetrics","1685370731986"
```

> Olhar pasta `output/log-groups-with-no-rotation/resources.json` para mais detalhes dos recursos filtrados.
