# Kubecost API + Grafana JSON Data Source

<img width="1435" alt="2023-02-23_10-00-55" src="https://user-images.githubusercontent.com/101200254/220944390-19392f7c-8464-4302-a160-387911d9e348.png">

## Overview

Kubecost is a Kubernetes cost allocation and optimization platform that provides cost visibility and allocation for workloads, clusters, namespaces, labels, and external cloud costs. It provides multiple API endpoints [https://docs.kubecost.com/apis/apis-overview] that allow users to access the cost, savings, and usage from Kubecost data in JSON or CSV formats.

Grafana is a popular open-source platform used for data visualization and monitoring. It supports a wide range of datasources, including JSON API, which allows you to connect Grafana to any RESTful API that returns data in JSON format.

The Kubecost Cost Model reconciles real-time metrics data alongside cloud billing data, and will adjust the on-demand costs to reflect your actual cloud provider bills. [https://docs.kubecost.com/install-and-configure/install/cloud-integration/multi-cloud]. The Kubecost JSON API allows you to access cost data which has been accurately reconciled with the cloud provider bills. 

The JSON APIs found at the ```/model``` URL endpoint allow you to pull the same cost data that is reflected via the Kubecost UI in the format of your choice.

In this guide, we will walk you through the steps to set up a JSON API datasource in Grafana to access the data collected by Kubecost.

## Prerequisites

- Kubecost installed and running in your Kubernetes cluster.
- Grafana instance installed and running.

## Steps to Set Up a JSON API Datasource for Kubecost in Grafana

Open your Grafana instance and navigate to the "Configuration" page from the left-hand menu.

- Click on the "Data Sources" option.

- Click on the "Add data source" button in the top right corner of the page.

- Select "JSON API" as the datasource type.

- Provide a name for the datasource in the "Name" field.

- In the "URL" field, enter the endpoint URL of the Kubecost API you want to connect to. The URL should be in the format: ```https://[Your-Kubecost-Domain]/model/[endpoint]```

<img width="793" alt="2023-02-23_09-55-40" src="https://user-images.githubusercontent.com/101200254/220943923-712701b4-0cbd-465b-8181-c2286eef3865.png">

- In the "Access" section, select the type of authentication you want to use (if any) to connect to the API. You can choose from "No Auth", "Basic Auth", and "Bearer Token".

- If you choose to use authentication, provide the necessary credentials or token in the fields provided.

- In the "HTTP settings" section, you can configure the HTTP method, request timeout, and headers.

- Scroll down to the "JSON API Query" section and provide the necessary parameters to query the Kubecost API. You can provide these queries and parameters at the datasource directly or provide them later during panel creation.

- Paramaters can be found in Kubecosts API docs [https://docs.kubecost.com/apis/apis-overview], JSONPath query examples can be found here: [https://github.com/kubecost/kubecost-grafana-json-integration/blob/main/kubecost-api-jsonpath-queries.md]

Once you have configured the datasource, click the "Save & Test" button at the bottom of the page to test the connection.

## Using the Kubecost API Datasource in Grafana

Once you have set up the Kubecost API datasource, you can use it to create dashboards and visualizations in Grafana. To use the datasource in a panel:

Create a new panel by clicking the "+" button on a dashboard.

- Select the visualization type you want to use.

- Click on the "Panel Data Source" dropdown menu and select the Kubecost API datasource you just created.

- Configure the panel settings, queries, and paramaters as needed.

<img width="1005" alt="2023-02-23_10-00-01" src="https://user-images.githubusercontent.com/101200254/220944212-f80b22a9-eccc-46e9-aa00-2165c5d168b0.png">

- Save the panel and add it to the dashboard.

- You can now use the Kubecost API data to create custom dashboards and visualizations in Grafana.
