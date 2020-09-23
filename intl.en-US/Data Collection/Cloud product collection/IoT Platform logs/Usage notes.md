# Usage notes

Alibaba Cloud IoT Platform provides the log dump feature. You can use this feature to dump logs from IoT Platform to Log Service. You can query, ship, and transform logs in real time in the Log Service console. You can also visualize the results of log analysis and configure alerts. This topic describes the resources, billing, and limits of loT Platform logs.

## Resources

-   Dedicated projects and Logstores

    After you enable the log dump feature, IoT Platform creates a project named iot-log-Alibaba Cloud account ID-Region ID and a Logstore named iot\_logs in the corresponding region.

-   Dedicated dashboards

    After you enable the log dump feature, a dashboard is generated by default.

    **Note:** The dedicated dashboard may be updated at any time. We recommend that you do not modify the dedicated dashboard. You can manually create a dashboard to visualize the results of log analysis. For more information, see [Create a dashboard](/intl.en-US/Query and visualization/Dashboard/Create a dashboard.md).

    |Dashboard|Description|
    |---------|-----------|
    |IoT operation center|Shows the statuses and errors of devices that are connected to loT Platform. You can view the number of times that you have logged on and off the devices, device IP addresses distributed by region, and error distribution for data parsing script. You can also view the error distribution for Thing Specification Language \(TSL\) validation, the number of forwarded subscription messages at the server side, the number of forwarded cloud service messages, and error distribution for API calls.|


## Billing

-   You are not billed when you use the log dump feature to dump logs.
-   However, you are billed based on the storage space usage, read traffic, number of requests, and the amount of transformed and shipped data. For more information, see [Log Service pricing](https://www.alibabacloud.com/product/log-service/pricing?spm=a3c0i.139163.9288850920.1.7690637avzyiqo).

## Limits

-   You can write only IoT Platform logs to a dedicated Logstore. You cannot modify the indexes of the Logstore.
-   You cannot delete dedicated projects or Logstores.
-   You can create only one log configuration file in each region. The operational logs of all cloud services in the region are automatically dumped to the dedicated Logstore based on the log collection configurations in the file.
-   The service is available only in the following regions: China \(Shanghai\), China \(Shenzhen\), Singapore \(Singapore\), Japan \(Tokyo\), Germany \(Frankfurt\), US \(Silicon Valley\), and US \(Virginia\).
