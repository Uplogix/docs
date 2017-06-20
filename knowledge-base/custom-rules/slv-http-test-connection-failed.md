These rules examine the results from an SLV (service level verification) test run by an Uplogix local manager for results that indicates that the test failed, and send email alerts to notify users subscribed to alerts on the Uplogix local manager in question.

To load them onto your Uplogix local manager, simply copy and paste the below rules into the CLI.

To apply the rules, attach them to a SLV test on the Uplogix local manager with the **config monitor** command (for example: **config monitor slv webtest httpSLVErrors :500**).

```
rule httpResponseZeroes
description this rule sends an alarm if the http slv test receives 0 for all round trip metrics
action alarm GENERIC -a "http test returned 0 on all metrics"
conditions
slv.timeToConnect equals 0 AND
slv.timeToFirstByte equals 0 AND
slv.timeToLastByte equals 0
exit
exit
 

rule httpResponseConnectionRefused
description this rule sends an alarm if the http slv test receives a 'connectionrefused' response
action alarm GENERIC -a "http test returned 'Connection refused'"
conditions
slv.message equals "Connection refused"
exit
exit

ruleset httpSLVErrors
description null
rules
httpResponseConnectionRefused | httpResponseZeroes
exit
exit
```