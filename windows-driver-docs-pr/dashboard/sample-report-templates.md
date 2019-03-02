---
title: 示例报告模板
description: 编译 Windows 驱动程序提交失败报告的示例报告模板。 代码是 REST API 和 JSON 格式。
ms.topic: article
ms.author: shganesh
ms.date: 09/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3ee53663a4c58346043d79d386aea5162eed268b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518447"
---
# <a name="sample-report-templates"></a>示例报告模板

本文包含几个报告模板，涵盖了常见业务需求的常见提交失败。 可以重复使用任何或这些模板，也可以根据业务需求对其进行自定义。

## <a name="request-syntax"></a>请求语法

|方法|请求 URI|
|----|----|
|POST|`https://manage.devcenter.microsoft.com/analytics/driver/reporttemplate`|

## <a name="request-headers"></a>请求标头

|标头|在任务栏的搜索框中键入|描述|
|----|----|----|
|授权|字符串|必需。 Azure AD 访问令牌的格式为 **Bearer** \<token\>|
|内容类型|字符串|Application/JSON|

## <a name="sample-1--show-all-available-columns-for-ihv-failure-details-for-the-last-7-days"></a>示例 1：显示过去 7 天的 IHV 失败详细信息的所有可用列

以下 API 请求有效负载列出了 IHV 失败报告中的所有可用列，并将 reportPeriod 设置为过去七天。

```json
{
   "view":"IHVDriver",
   "projection":[
      "ReportId",
      "FailureDate",
      "FailureDateTime",
      "ApplicationId",
      "SubmissionId",
      "FailureName",
      "FailureHash",
      "Symbol",
      "OSVersion",
      "OSName",
      "EventType",
      "Market",
      "DeviceType",
      "DriverName",
      "DriverVersion",
      "Architecture",
      "OEMName",
      "OEMModel",
      "FlightRing",
      "Mode",
      "CPUName",
      "OSSKUType",
      "ReleaseName",
      "CabType",
      "CabIdHash",
      "CabExpirationTime",
      "DeviceId",
      "HardwareId",
      "CabCollectionTime",
      "EventCount"
   ],
   "dateRange":{
      "reportPeriod":"Last7Days"
   }
}
```

## <a name="sample-2-show-all-available-columns-for-oem-failure-details-for-the-last-7-days"></a>示例 2：显示过去 7 天的 OEM 失败详细信息的所有可用列

以下 API 请求有效负载列出了 OEM 失败报告中的所有可用列，并将 reportPeriod 设置为过去七天。

```json
{
   "view":"OEMDriver",
   "projection":
  [
      "ReportId",
      "FailureDate",
      "FailureDateTime",
      "FailureName",
      "FailureHash",
      "Symbol",
      "OSVersion",
      "EventType",
      "Market",
      "DeviceType",
      "DriverName",
      "DriverVersion",
      "Architecture",
      "Model",
      "Baseboard",
      "ModelFamily",
      "FlightRing",
      "Mode",
      "CPUName",
      "OSSKUType",
      "ReleaseName",
      "CabType",
      "CabIdHash",
      "CabExpirationTime",
      "DeviceId",
      "HardwareId",
      "CabCollectionTime",
      "EventCount"
   ],
   "dateRange":{
      "reportPeriod":"Last7Days"
   }
}
```

## <a name="sample-3--show-the-number-of-ihv-failures-the-unique-devices-impacted-for-each-driver-over-the-last-30-days-and-sort-by-devices-impacted"></a>示例 3：显示过去 30 天内 IHV 失败的次数、每个驱动程序影响的唯一设备，并按受影响的设备排序

此 API 请求有效负载调用 IHV 失败报告，该报告列出过去 30 天内报告的驱动程序失败总数以及每个驱动程序影响的唯一设备。 它按受影响的设备对报告进行排序。

```json
{
   "view":"IHVDriver",
   "projection":
  [
      "DriverName",
      "DriverVersion",
      "FailureName",
      "FailureHash"
   ],
   "dateRange":{
      "reportPeriod":"Last30Days"
   },
   "aggregation":{
      "aggregatedColumns":[
         "SUM(EventCount)",
         "DCOUNT(DeviceId)"
      ]
   },
   "orderby":[
      {
         "attribute":"DCOUNT(DeviceId)",
         "sort":"desc"
      }
   ]
}
```

## <a name="sample-4-list-the-number-of-oem-failure-details-over-the-past-seven-days-for-which-the-number-of-kernel-crashes-is-greater-than-1000"></a>示例 4：列出过去 7 天内 OEM 失败的详细信息，其中内核崩溃的数量大于 1000

此 API 请求有效负载调用 OEM 失败报告，该报告列出过去 7 天内报告的所有失败，并按在此期间发生超过 1000 次内核崩溃的失败进行筛选。

```json
{
   "view":"OEMDriver",
   "projection":[
      "FailureName",
      "FailureHash"
   ],
   "dateRange":{
      "reportPeriod":"Last7Days"
   },
   "condition":{
      "and":[
         {
            "attribute":"EventType",
            "operator":"eq",
            "value":"Kernel"
         }
      ]
   },
   "aggregation":{
      "aggregatedColumns":[
         "SUM(EventCount)"
      ],
      "condition":{
         "or":[
            {
               "attribute":"SUM(EventCount)",
               "operator":"gt",
               "value":"1000"
            }
         ]
      }
   }
}
```

## <a name="sample-5-list-the-top-10-drivers-that-impact-the-maximum-number-of-unique-devices-in-the-last-90-days"></a>示例 5：列出在过去 90 天内影响唯一设备最大数量的前 10 个驱动程序

此 API 请求有效负载调用所有驱动程序的 IHV 失败报告。 然后，它会根据受失败影响的设备数量对列表进行聚合和排序，并显示影响设备的前十个驱动程序。

```json
{
  "view": "IHVDriver",
  "projection": [
    "DriverName"
  ],
  "dateRange": {
    "reportPeriod": "Last90Days"
  },
  
  "aggregation": {
    "aggregatedColumns": [
      "DCOUNT(DeviceId)"
    ]
  },
  "orderby": [
      {
        "attribute": "DCOUNT(DeviceId)",
        "sort": "desc"
      }
    ],
    "limit": 10  
}
```

## <a name="see-also"></a>另请参阅

- [创建新的报告模板](create-a-new-report-template.md)

- [分析报告 API (Swagger)](https://apidocs.microsoft.com/services/analyticsreportingapis)

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
