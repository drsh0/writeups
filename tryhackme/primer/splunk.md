# Splunk

## Scenario 1
#### Notable Commands

metadata

stats – distinct count, count, values, average, AS

* Distinct count -- `stats dc(field)`

lookup
* Do note that character case matters in lookups. Best to use `lower()` with unknown data. 

* `lookup` can compare a field from one file with fiend values found in data -- `lookup file.csv FileField as CompareToField OUTPUTNEW NewDisplayField `

eval – lower, length, round

fields

table

AND OR NOT

sort

reverse

transaction

* Groups events. One use case is to see a difference in time between two events: `transaction <InterestingFields> | table duration`

rex

search

inputlookup



outputlookup


#### Useful OSINT Tools

* Threatminer
* Hybrid-Analysis
* ThreatCrowd