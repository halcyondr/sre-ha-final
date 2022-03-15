# API Service

| Category     | SLI | SLO                                                                                                         |
|--------------|-----|-------------------------------------------------------------------------------------------------------------|
| Availability | total # of successful requests / total # of requests   | 99%                                                                                                         |
| Latency      | 90th percentile latency over a 5 min period | 90% of requests below 100ms                                                                                 |
| Error Budget | the number of error requests/total number of requests for the period of the budget | Error budget is defined at 20%. This means that 20% of the requests can fail and still be within the budget |
| Throughput   | total number of requests over a period of time  | 5 RPS indicates the application is functioning                                                              |
