# Using JSONPath Queries with the Kubecost API

To use the Grafana JSON plugin with the Kubecost REST API that returns nested JSON, you'll need to use JSONPath queries to extract the data you want to visualize in Grafana. Here's a step-by-step guide on how to do it:

- Install and configure the Grafana JSON plugin. You can find installation instructions and documentation on the official Grafana website.

- Connect to your Kubecost REST API endpoint (/model/allocation, /model/assets, etc - See Kubecost API Docs) by adding it as a data source in Grafana. You'll need to provide the API endpoint URL, method, and any authentication details required.

- Once you've connected to the API, create a new dashboard in Grafana and add a panel.

In the panel settings, select the JSON data source you just created and enter your JSONPath query in the "JSONPath Expression" field. This is where you'll specify which parts of the JSON response to extract and display in the panel.

<img width="975" alt="2023-02-23_07-52-28" src="https://user-images.githubusercontent.com/101200254/220920076-d5f64dc1-5972-4183-8c0b-a3c44d3cd288.png">

Save the panel and view your data in Grafana!

Here are some examples of JSONPath queries you can use to extract data from a nested JSON response:

## JSONPath Examples

JSONPath is a query language used to access parts of a JSON document. Here are some examples of JSONPath queries you can use to extract data from a nested JSON response:

### Example 1: Extract a single value from a nested object

Suppose your Kubecost /model/allocation API returns data that looks like this:
```
{
    "code": 200,
    "data": [
        {
            "kc-demo-dev": {
                "name": "kc-demo-dev",
                "properties": {
                    "cluster": "kc-demo-dev"
                },
                "window": {
                    "start": "2023-02-17T00:00:00Z",
                    "end": "2023-02-24T00:00:00Z"
                },
                "start": "2023-02-17T00:00:00Z",
                "end": "2023-02-23T13:00:00Z",
                "minutes": 9420.000000,
                "cpuCores": 2.288715,
                "cpuCoreRequestAverage": 2.279277,
                "cpuCoreUsageAverage": 0.110639,
                "cpuCoreHours": 359.328295,
                "cpuCost": 11.358727,
                "cpuCostAdjustment": 0.000000,
                "cpuEfficiency": 0.048541,
                "gpuCount": 0.000000,
                "gpuHours": 0.000000,
                "gpuCost": 0.000000,
                "gpuCostAdjustment": 0.000000,
                "networkTransferBytes": 0.000000,
                "networkReceiveBytes": 0.000000,
                "networkCost": 0.506502,
                "networkCrossZoneCost": 0.000000,
                "networkCrossRegionCost": 0.000000,
                "networkInternetCost": 0.506502,
                "networkCostAdjustment": 0.000000,
                "loadBalancerCost": 1.690000,
                "loadBalancerCostAdjustment": -0.100147,
                "pvBytes": 68238283274.452393,
                "pvByteHours": 10713410474089.025391,
                "pvCost": 0.546720,
                "pvs": {
                    "cluster=kc-demo-dev:name=pvc-02525fec-eadb-45ae-936c-b5a79e875df2": {
                        "byteHours": 5353291288681.026,
                        "cost": 0.2731858068923077
                    },
                    "cluster=kc-demo-dev:name=pvc-35073d25-0e2d-4e32-8c34-2757ce4f7103": {
                        "byteHours": 5360119185407.999,
                        "cost": 0.2735342438399999
                    }
                },
                "pvCostAdjustment": 0.475405,
                "ramBytes": 3267940462.346716,
                "ramByteRequestAverage": 2564047717.639066,
                "ramByteUsageAverage": 2143588143.301442,
                "ramByteHours": 513066652588.434387,
                "ramCost": 2.024568,
                "ramCostAdjustment": 0.000000,
                "ramEfficiency": 0.836017,
                "sharedCost": 0.000000,
                "externalCost": 0.000000,
                "totalCost": 16.501775,
                "totalEfficiency": 0.167667,
                "rawAllocationOnly": null
            },
        }
    ]
}
```
You can use the following JSON Path queries:
```
$.data:
```
This will return the entire data array.
```
$.data[0]
```
This will return the first object in the data array.

```
$.data[0]['kc-demo-dev']:
``` 
This will return the object with the key kc-demo-dev in the first object of the data array.
```
$.data[*]['kc-demo-dev'].name
``` 
This will return the value of the name property for all objects with the key kc-demo-dev in the data array.
```
$.data[*]['kc-demo-dev'].ramCost
``` 
This will return the value of the ramCost property for all objects with the key kc-demo-dev in the data array.

These are just a few examples, and there are many more JSONPath queries that can be used depending on the specific data you want to extract from the JSON payload.

### Example 2: Extract an array of values from a nested object

For an example, the Kubecost /allocation/external API returns data that looks like this: 
```
{
    "code": 200,
    "data": {
        "totals": {
            "cpuCost": 84.7816763860236,
            "gpuCost": 0,
            "ramCost": 20.03441570761475,
            "pvCost": 8.034883014006816,
            "networkCost": 2.6666288069161306,
            "loadBalancerCost": 20.03441570761475,
            "sharedCost": 0,
            "externalCost": 7688.6793545986975,
            "totalCost": 7848.042958581807,
            "efficiency": 0.2536369864818728
        },
        "items": [
            {
                "name": "sales demo",
                "cpuCost": 0,
                "gpuCost": 0,
                "ramCost": 0,
                "pvCost": 0,
                "networkCost": 0,
                "loadBalancerCost": 0,
                "sharedCost": 0,
                "externalCost": 108.0967975893,
                "totalCost": 108.0967975893,
                "efficiency": 0,
                "externalBreakdown": [
                    {
                        "name": "AmazonEC2",
                        "cost": 85.60443103509999
                    },
                    {
                        "name": "AWSLambda",
                        "cost": 0
                    },
                    {
                        "name": "AmazonS3",
                        "cost": 8.4923665542
                    },
                    {
                        "name": "AmazonEKS",
                        "cost": 14.000000000000002
                    }
                ]
            }
```

To extract an array of amount values from the orders array, you can use the following JSONPath query:
```
$.data.items[*].totalCost
```
This will return an array of numbers [108.0967975893,<totalCost2>,<totalCost3>].

You can experiment with different JSONPath queries and panel types to create different types of visualizations, depending on the data you're working with.
