# kubecost-grafana-json-integration
Use Kubecost API as a Grafana JSON data source.

# How to Use Kubecost API with Grafana JSON Datasource

Kubecost is a Kubernetes cost allocation and optimization platform that provides cost visibility and allocation for workloads, clusters, and namespaces. It provides an API that allows you to access the data collected by Kubecost.

Grafana is a popular open-source platform used for data visualization and monitoring. It supports a wide range of datasources, including JSON API, which allows you to connect Grafana to any RESTful API that returns data in JSON format.

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

- In the "URL" field, enter the endpoint URL of the Kubecost API you want to connect to. The URL should be in the format: https://[Your-Kubecost-Domain]/model/[endpoint]

- In the "Access" section, select the type of authentication you want to use (if any) to connect to the API. You can choose from "No Auth", "Basic Auth", and "Bearer Token".

- If you choose to use authentication, provide the necessary credentials or token in the fields provided.

- In the "HTTP settings" section, you can configure the HTTP method, request timeout, and headers.

- Scroll down to the "JSON API Query" section and provide the necessary parameters to query the Kubecost API. You can use the following parameters to retrieve cost data:

[Example]

Once you have configured the datasource, click the "Save & Test" button at the bottom of the page to test the connection.

## Using the Kubecost API Datasource in Grafana

Once you have set up the Kubecost API datasource, you can use it to create dashboards and visualizations in Grafana. To use the datasource in a panel:

Create a new panel by clicking the "+" button on a dashboard.
- Select the visualization type you want to use.

- Click on the "Panel Data Source" dropdown menu and select the Kubecost API datasource you just created.

- Configure the panel settings and queries as needed.

- Save the panel and add it to the dashboard.

- You can now use the Kubecost API data to create custom dashboards and visualizations in Grafana.
