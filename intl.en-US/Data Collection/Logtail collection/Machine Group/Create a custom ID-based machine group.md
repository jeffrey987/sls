# Create a custom ID-based machine group

Log Service allows you to create a custom ID-based machine group. This topic describes how to create a custom ID-based machine group in the Log Service console.

-   A project and a Logstore are created. For more information, see [Create a project and a Logstore](/intl.en-US/.md).
-   At least one server is available.
    -   If you use an ECS instance, you must ensure that the ECS instance and Log Service project share the same Alibaba Cloud account and belong to the same region.
    -   If the ECS instance is purchased by another Alibaba Cloud account, you must configure a user identifier before you create an IP address-based machine group. If the server is provided by another cloud service vendor or is deployed in a user-created data center, you must also perform the preceding operation. For more information, see [Configure an account ID for a server](/intl.en-US/Data Collection/Logtail collection/Machine Group/Configure an account ID for a server.md).
-   Logtail is installed on the server. For more information, see [Install Logtail on ECS instances](/intl.en-US/Data Collection/Logtail collection/Install/Install Logtail on ECS instances.md).

Custom ID-based machine groups offer significant benefits in the following scenarios:

-   If your servers reside in multiple custom network environments such as virtual private clouds \(VPCs\), some IP addresses of the servers may conflict. In this case, Logtail cannot collect logs as expected. You can use a custom ID to prevent this issue.
-   If you want to add multiple servers to a machine group, you can set the same custom ID for new servers as the machine group. Log Service identifies the custom ID and adds the servers with the same custom ID to the machine group.

## Procedure

1.  Create a file named user\_defined\_id in a specified directory.

    -   Linux: Store the file in the /etc/ilogtail/user\_defined\_id directory.
    -   Windows: Store the file in the C:\\LogtailData\\user\_defined\_ided\_id directory.
2.  Set a custom ID for the server.

    **Note:**

    -   Windows and Linux servers cannot be added to the same machine group. You cannot set the same custom ID for Linux and Windows servers.
    -   You can set one or more custom IDs for a single server and separate custom IDs with line feeds.
    -   In the Linux server, if the /etc/ilogtail/ directory or the /etc/ilogtail/user\_defined\_id file does not exist, you can create the directory and file. In the Windows server, if the C:\\LogtailData directory or the C:\\LogtailData\\user\_defined\_id file does not exist, you can also create the directory and file.
    -   Linux:

        Set the custom ID in the /etc/ilogtail/user\_defined\_id file. For example, if you want to set the custom ID to `userdefined`, run the following command to edit the file. In the file, enter `userdefined`.

        ```
        vim /etc/ilogtail/user_defined_id
        ```

    -   Windows:

        Set the custom ID in the C:\\LogtailData\\user\_defined\_id file. For example, if you want to set the custom ID to `userdefined_windows`, enter `userdefined_windows` in the C:\\LogtailData\\user\_defined\_id file.

3.  Log on to the [Log Service console](https://sls.console.aliyun.com).

4.  In the Projects section, click the destination project.

5.  In the left-side navigation pane, click **Machine Groups**.

6.  On the right of the **Machine Groups**, choose **![Machine groups](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2123359951/p52484.png)** \> **Create Machine Group**.

7.  In the Create Machine Group dialog box, set the required parameters, and then click **OK**. The following table describes the parameters.

    |Parameter|Description|
    |---------|-----------|
    |Name|The name of the machine group. The name must be 2 to 128 characters in length, and can contain only lowercase letters, digits, hyphens \(-\), and underscores \(\_\). The name must start and end with a lowercase letter or digit. **Note:** After the machine group is created, you cannot modify its name. Proceed with caution. |
    |Identifier|The identifier of the server. Select **Custom ID**.|
    |Topic|The topic of the machine group. This topic is used to differentiate log data that is generated in different servers. For more information, see [Configure a log topic](/intl.en-US/Data Collection/Logtail collection/Text logs/Configure a log topic.md).|
    |Custom Identifier|Enter the custom ID that is set in [2](#step_y5a_p7f_25u).|

8.  View the status of the machine group.

    1.  In the list of machine groups, click the destination machine group.

    2.  On the Machine Group Settings page, view the status of the machine group. You can view the list of servers that share the same custom ID. You can also view the heartbeat statuses of these servers.

        -   The Machine Group Status section lists the IP addresses of the servers whose custom ID is the same as the custom ID that you set for the machine group.

            For example, the custom ID of a machine group is userdefined and the IP addresses in the Machine Group Status section are 10.10.10.10, 10.10.10.11, and 10.10.10.12. This indicates that you have specified the same custom ID for the servers in this machine group. If you want to add another server to the machine group and the IP address of the server is 10.10.10.13, set the custom ID to userdefined for the server. Then, you can view the IP address of the added server in the Machine Group Status section.

        -   If the **Heartbeat** status is **OK**, the server is connected to Log Service. If the status is **FAIL**, see [What can I do if the Logtail client has no heartbeat?]()
        ![Machine group status](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2123359951/p5255.png)


## Disable a custom ID

If you want to set the Identifier parameter to IP Addresses, delete the user\_defined\_id file. The new configurations take effect within 1 minute.

-   In Linux, run the following command:

    ```
    rm -f /etc/ilogtail/user_defined_id
    ```

-   In Windows, run the following command:

    ```
    del C:\LogtailData\user_defined_id
    ```


## Time to take effect

By default, after you add, delete, or modify the user\_defined\_id file, the new configurations take effect within 1 minute. If you want the configurations to immediately take effect, run the following command to restart Logtail.

-   Linux:

    ```
    /etc/init.d/ilogtaild stop
    /etc/init.d/ilogtaild start
    ```

-   Windows:
    1.  Choose **Start Menu** \> **Control Panel** \> **Administrative Tools** \> **Services**.
    2.  In the Services window, select the required service.
        -   For Logtail V0.x.x.x, select LogtailWorker.
        -   For Logtail V1.0.0.0 or later, select LogtailDaemon.
    3.  Right-click the service and then select **Restart** to validate the configurations.

