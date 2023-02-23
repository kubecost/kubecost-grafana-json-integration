#Using JSONPath and JSONata with Kubecost API

## JSONPath Examples

JSONPath is a query language used to access parts of a JSON document. Here are some examples of JSONPath queries you can use to retrieve data from the Kubecost allocation API:

### Retrieve all namespaces
```
$.namespaces[*].namespace
```
This query retrieves all the namespaces available in the allocation data.

### Retrieve total cost for a specific namespace
```
$.namespaces[?(@.namespace == 'your-namespace')].cost
```
This query retrieves the total cost for a specific namespace.

### Retrieve cost data for a specific namespace over a time range
```
$.namespaces[?(@.namespace == 'your-namespace')].pods[*].costs[?(@.start_time >= start_timestamp && @.end_time <= end_timestamp)]
```
This query retrieves cost data for a specific namespace over a specified time range. You'll need to replace your-namespace, start_timestamp, and end_timestamp with the appropriate values.

## JSONata Examples
JSONata is a query and transformation language for JSON documents. Here are some examples of JSONata queries you can use to retrieve data from the Kubecost allocation API:

### Retrieve all namespaces
```
namespaces.namespace
```
This query retrieves all the namespaces available in the allocation data.

### Retrieve total cost for a specific namespace
```
namespaces.{
  namespace: $$.namespace,
  cost: $$.cost
}[namespace = 'your-namespace'].cost
```
This query retrieves the total cost for a specific namespace.

```
namespaces.{
  namespace: $$.namespace,
  costs: pods.[{
    name: $$.name,
    cost: costs[($$.start_time >= start_timestamp) and ($$.end_time <= end_timestamp)].cost
  }][cost != null]
}[namespace = 'your-namespace']
```
This query retrieves cost data for a specific namespace over a specified time range. You'll need to replace your-namespace, start_timestamp, and end_timestamp with the appropriate values.
