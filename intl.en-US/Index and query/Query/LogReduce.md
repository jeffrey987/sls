# LogReduce

This topic describes how to use the LogReduce feature of Log Service. You can enable the feature, view log clustering results and raw logs, adjust clustering precision, and compare the number of log entries in different time periods.

The LogReduce feature allows you to cluster similar logs and extract patterns from the logs. You can use this feature to cluster text logs of multiple formats. You can use this feature to locate errors, detect anomalies, roll back versions, and perform other O&M operations in DevOps scenarios. You can also use this feature to detect network intrusions to ensure data security. In addition, you can save log clustering results as charts to a dashboard, and then view the clustered data in real time.

## Benefits

-   You can cluster logs of multiple formats, such as Log4j logs, JSON-formatted logs, and single-line logs.
-   Hundreds of millions of log entries can be clustered in seconds.
-   Log data can be clustered in multiple modes.
-   Raw log data can be retrieved based on pattern signatures.
-   You can compare log patterns of different time periods.
-   You can adjust the clustering precision of logs.

## Indexes

If you enable the LogReduce feature, the size of indexes increases by 10% of the raw log size. For example, if the size of the raw log data is 100 GB per day, the size of indexes increases by 10 GB.

|Raw log size|Index percentage|Size of indexes that are generated by LogReduce|Index size|
|:-----------|:---------------|:----------------------------------------------|:---------|
|100 GB|20% \(20 GB\)|100 \* 10%|30 GB|
|100 GB|40% \(40 GB\)|100 \* 10%|50 GB|
|100 GB|100% \(100 GB\)|100 \* 10%|110 GB|

## Enable LogReduce of a Logstore

1.  Log on to the [Log Service console](https://sls.console.aliyun.com).

2.  In the Projects section, click the destination project.

3.  On the **Log Storage** \> **Logstores** tab, click the destination Logstore.

4.  Enable the LogReduce feature.

    1.  Choose **Index Attributes** \> **Modify**.

        If the indexing feature is not enabled, click **Enable**.

    2.  In the Search & Analysis dialog box, turn on the LogReduce switch.

    3.  Optional. Configure a whitelist or blacklist to filter fields.

        You can filter logs by keyword. Logs that are filtered based on keywords are automatically clustered.

    4.  Click **OK**.


## View log clustering results and raw logs

1.  On the Search & Analysis page, enter a search statement in the search box, and then click **Search & Analyze**.

    **Note:** You can use only search statements to filter logs. You cannot use analytic statements to analyze logs because the LogReduce feature cannot cluster analysis results.

2.  Click the **LogReduce** tab to view the log clustering results.

    ![Log clustering details](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6523359951/p34195.png)

    |Parameter|Description|
    |:--------|:----------|
    |**Number**|The sequence number of a log cluster.|
    |**Count**|The number of log entries in a pattern. The log entries are obtained in the current time range.|
    |**Pattern**|The log pattern. Each log cluster has one or more sub-patterns.|

    -   Move the pointer over a value in the **Count** column to view the sub-patterns of the corresponding log cluster and percentage of each sub-pattern in the log cluster. Click the plus sign \(+\) next to the value to expand the sub-pattern list.
    -   Click a value in the **Count** column. You are redirected to the Raw Logs tab. On this tab, you can view the raw logs of the corresponding pattern.

## Adjust the precision of log clustering

On the **LogReduce** tab, you can drag the **Pattern Count** slider to adjust the clustering precision.

-   If you drag the slider towards **Many**, you can obtain a more precise log clustering result with more detailed patterns.
-   If you drag the slider towards **Little**, you can obtain a less precise log clustering result with fewer detailed patterns.

## Compare the number of log entries that are clustered in different time periods

1.  On the **LogReduce** tab, click **Log Compare**.

2.  Set a time range, and then click **OK**.

    For example, if you set the time range to 15 minutes when you perform a query, and select **1 Day** for **Log Compare**, the start time and end time for log comparison are displayed. The time range is 15 minutes.

    ![Compare the number of log entries](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6523359951/p34223.png)

    |Parameter|Description|
    |---------|-----------|
    |Number|The sequence number of a log group.|
    |Pre\_Count|The number of log entries of a pattern that are obtained in the time range specified by **Log Compare**.|
    |Count|The number of log entries in a pattern. The log entries are obtained in the current time range.|
    |Diff|The difference between the number of log entries that are specified by the Pre\_Count and Count parameters and the growth rate.|
    |Pattern|The log pattern.|


## Examples

You can use search and analytic statements to query clustered log data.

-   Obtain log clustering results.
    -   Search and analytic statement

        ```
        * | select a.pattern, a.count,a.signature, a.origin_signatures from (select log_reduce(3) as a from log) limit 1000 
        ```

        **Note:** When you view log clustering results, you can click **Copy Query** to obtain the search and analytic statement.

    -   Modify parameter settings

        In the search and analytic statement, the log\_reduce\(precision\) function specifies the clustering precision. Valid values: 1 to 16. A smaller value indicates a higher clustering precision and more patterns. Default value: 3.

    -   Returned fields

        You can view the clustering details on the Graph tab.

        |Parameter|Description|
        |---------|-----------|
        |pattern|The log pattern.|
        |count|The number of log entries in a pattern. The log entries are obtained in the current time range.|
        |signature|The signature of the log pattern.|
        |origin\_signatures|The secondary signature of the log pattern. You can use this signature to query corresponding raw data.|

-   Compare the number of log entries that are clustered in different time periods.
    -   Search and analytic statement

        ```
        * | select v.pattern, v.signature, v.count, v.count_compare, v.diff from (select compare_log_reduce(3, 86400) as v from log) order by v.diff desc limit 1000 
        ```

        **Note:** When you use **Log Compare** to compare log clustering results in different time periods, you can click **Copy Query** to obtain the search and analytic statement.

    -   Modify parameter settings

        Modify parameter settings in the compare\_log\_reduce\(precision, compare\_interval\) function.

        -   The precision parameter specifies the clustering precision. Valid values: 1 to 16. A smaller number indicates a higher clustering precision and more patterns. Default value: 3.
        -   The compare\_interval parameter specifies the time difference between the two time ranges when the number of log entries are compared. The value is a positive integer. Unit: seconds.
    -   Returned fields

        |Parameter|Description|
        |---------|-----------|
        |pattern|The log pattern.|
        |count\_compare|The number of log entries in a pattern that are obtained in the time range specified by Log Compare.|
        |count|The number of log entries in a pattern. The log entries are obtained in the current time range.|
        |diff|The difference between the number of log entries that are indicated by the count and count\_compare fields.|
        |signature|The signature of the log pattern.|


## Enable LogReduce of a Logstore

If you no longer need this feature, you can disable it.

1.  On the Search and Analysis page of the Logstore for which you want to disable the feature, choose **Index Attributes** \> **Modify**.

2.  Turn off the **LogReduce** switch.

3.  Click **OK**.


