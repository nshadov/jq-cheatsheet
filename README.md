# JQ CheatSheet
My small JSON parsing Cheat Sheet for JQ

## All available tags arrays:

```
cat file.json | jq -C '.[].tags'
```

## All availbe tags (extracted from arrays):

```
cat file.json | jq -C '.[].tags[]'
```

## Tags array does NOT contain "BLOCKED":

```
cat file.json | jq -C '(. - map(select(.tags[] | contains("BLOCKED"))) )'
```

## Tags array contains "BLOCKED":

```
cat file.json | jq -C '.[] | select(.tags[] | contains("BLOCKED"))'
```

## Interactions of type "action"

```
cat interactions.raw | ./parse_interactions.py | jq -C '.[] | select(.row.type | contains("action"))'
```

## Only timestamps of these

```
cat file.json | jq -C '.[] | select(.tags[] | contains("BLOCKED")) | .timestamp'
```

## Field timestamp contains:

```
cat file.json | jq -C '.[] | select(.timestamp | contains("2017-01-01T12:30"))'
```

## Counting things

```
cat file.json | jq -C '.["ip"] | length'
```

## Return Multiple fields

```
aws --profile=production route53 list-resource-record-sets --hosted-zone-id *** | jq -C '.[][] | "\(.Name) \(.Type))"'
```

## Field does not exist ("Cannot iterate over null")

```
aws --profile=production route53 list-resource-record-sets --hosted-zone-id *** | jq -C '.[][] | "\(.Name) \(.Type) \(.ResourceRecords[]?.Value)"' | less
```
