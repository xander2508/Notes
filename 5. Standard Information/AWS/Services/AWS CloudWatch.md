CloudWatch is a monitoring and observability service that collects your resource data and provides actionable insights into your applications. With CloudWatch, you can respond to system-wide performance changes, optimize resource usage, and get a unified view of operational health.

You can use CloudWatch to do the following:

- Detect anomalous behaviour in your environments.
- Set alarms to alert you when something is not right.
- Visualize logs and metrics with the AWS Management Console.
- Take automated actions like scaling.
- Troubleshoot issues.
- Discover insights to keep your applications healthy.

Many AWS services automatically send metrics to CloudWatch for free at a rate of 1 data point per metric per 5-minute interval. This is called basic monitoring, and it gives you visibility into your systems without any extra cost. For many applications, basic monitoring is adequate.  
  
For applications running on EC2 instances, you can get more granularity by posting metrics every minute instead of every 5-minutes using a feature like detailed monitoring. Detailed monitoring incurs a fee.

## CloudWatch concepts

Metrics are the fundamental concept in CloudWatch. A metric represents a time-ordered set of data points that are published to CloudWatch. Think of a metric as a variable to monitor and the data points as representing the values of that variable over time. Every metric data point must be associated with a timestamp.

AWS services that send data to CloudWatch attach dimensions to each metric. A dimension is a name and value pair that is part of the metric’s identity. You can use dimensions to filter the results that CloudWatch returns. For example, many Amazon EC2 metrics publish `InstanceId` as a dimension name and the actual instance ID as the value for that dimension.

By default, many AWS services provide metrics at no charge for resources such as EC2 instances, Amazon Elastic Block Store (Amazon EBS) volumes, and Amazon RDS database (DB) instances. For a charge, you can activate features such as detailed monitoring or publishing your own application metrics on resources such as your EC2 instances.

## Custom metrics

With custom metrics, you can publish your own metrics to CloudWatch.  
  
If you want to gain more granular visibility, you can use high-resolution custom metrics, which make it possible for you to collect custom metrics down to a 1-second resolution. This means you can send 1 data point per second per custom metric.

## CloudWatch dashboards

Dashboards are customizable home pages you can configure for data visualization for one or more metrics through widgets, such as a graph or text.

You can build many custom dashboards, each one focusing on a distinct view of your environment. You can even pull data from different AWS Regions into a single dashboard to create a global view of your architecture.

CloudWatch aggregates statistics according to the period of time that you specify when creating your graph or requesting your metrics. You can also choose whether your metric widgets display live data. Live data is data published within the last minute that has not been fully aggregated.

You are not bound to using CloudWatch exclusively for all your visualization needs. You can use external or custom tools to ingest and analyse CloudWatch metrics using the `GetMetricData` API.  
  
As far as security is concerned, with [[IAM Policies]], you control who has access to view or manage your CloudWatch dashboards.

## Amazon CloudWatch Logs  

CloudWatch Logs is centralized place for logs to be stored and analysed. With this service, you can monitor, store, and access your log files from applications running on [[Amazon EC2 Instance Store]] instances, [[AWS Lambda]] functions, and other sources.

With CloudWatch Logs, you can query and filter your log data. You can set up metric filters on logs, which turn log data into numerical CloudWatch metrics that you can graph and use on your dashboards.

Some services, like Lambda, are set up to send log data to CloudWatch Logs with minimal effort. With Lambda, all you need to do is give the Lambda function the correct IAM permissions to post logs to CloudWatch Logs. Other services require more configuration. For example, to send your application logs from an EC2 instance into CloudWatch Logs, you need to install and configure the CloudWatch Logs agent on the EC2 instance. With the CloudWatch Logs agent, EC2 instances can automatically send log data to CloudWatch Logs.

## CloudWatch Logs terminology  

A log event is a record of activity recorded by the application or resource being monitored. Events contain a timestamp and a event message.

Log events are grouped into log streams all belonging to the same source.

Log group is composed of log streams which all share the same retention and permission settings.

## CloudWatch alarms

You can create CloudWatch alarms to automatically initiate actions based on sustained state changes of your metrics. You configure when alarms are invoked and the action that is performed.

Actions can be an Amazon EC2 action, an automatic scaling action, or a notification sent to Amazon Simple Notification Service (Amazon SNS).

Alarms have three states: OK, ALARM, INSUFFICIEN_DATA

