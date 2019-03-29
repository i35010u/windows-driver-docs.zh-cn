---
title: 管理报告模板和计划报告
description: 使用这些 API 可以查看和修改现有 Windows 驱动程序提交报告模板以及管理计划报告
ms.topic: article
ms.author: shganesh
ms.date: 09/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: fe1a9e9acd4d39e4940872d8bbf425e848e54a59
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463945"
---
# <a name="manage-report-templates-and-scheduled-reports"></a>管理报告模板和计划报告

使用这些方法可以查看、修改现有报告模板并管理计划报告。

## <a name="request-headers"></a>请求标头

|标头|在任务栏的搜索框中键入|描述|
|----|----|----|
|授权|字符串|必需。 采用 **Bearer** \<令牌\> 格式的 Azure AD 访问令牌|
|内容类型|字符串|Application/JSON|

## <a name="view-a-definition-of-a-report-template"></a>查看报告模板的定义

使用此方法可以查看报告模板的定义。

<table>
  <thead>
    <tr>
      <th>项目</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>GET</td>
      <td><pre>https://manage.devcenter.microsoft.com/analytics/driver/reporttemplate/{templateId}</pre></td>
    </tr>
    <tr>
      <td>响应代码</td>
      <td>200/500/400</td>
    </tr>
    <tr>
      <td>响应有效负载</td>
      <td><pre>{
    "data": {
        "templateId": &lt;templateid&gt;
        " template": "{report template}”,
    "errors": []
}</pre></td>
    </tr>
  </tbody>
</table>

## <a name="view-all-available-report-templates"></a>查看所有可用的报告模板

使用此方法可以查看你为帐户创建的所有报告模板。

<table>
  <thead>
    <tr>
      <th>项目</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>GET</td>
      <td><pre>https://manage.devcenter.microsoft.com/analytics/driver/reporttemplate</pre></td>
    </tr>
    <tr>
      <td>响应代码</td>
      <td>200/500/400</td>
    </tr>
    <tr>
      <td>响应有效负载</td>
      <td><pre>{
    "data": [
        {
            "templateId": &lt;templateid&gt;,
            "template": "{report template}",
            "createdDatetime": "2018-06-24T16:39:46.683",
            "modifiedDatetime": "2018-06-24T16:39:46.683"
        }
        {
            "templateId": &lt;templateid&gt;,
            "template": "{report template}",
            "createdDatetime": "2018-06-27T14:09:27.243",
            "modifiedDatetime": "2018-06-27T14:09:32.733"
        }
],
    "errors": []
}
</pre></td>
    </tr>
  </tbody>
</table>

## <a name="edit-a-report-template"></a>编辑报告模板

使用此方法可以编辑现有报告模板。

<table>
  <thead>
    <tr>
      <th>项目</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST</td>
      <td><pre>https://manage.devcenter.microsoft.com/analytics/driver/reporttemplate/{templateId}</pre></td>
    </tr>
    <tr>
      <td>示例有效负载</td>
      <td><pre>{<br/>   "view":"IHVDriver",
   "projection":[<br/>      "EventType",
      "DriverName"
   ],
   "dateRange":{<br/>      "reportPeriod":"Yesterday"
   },
   "condition":{  

   },
   "aggregation":{  
      "aggregatedColumns":[  
         "sum(EventCount)"
      ]
   }
}</pre></td>
    </tr>
    <tr>
      <td>响应代码</td>
      <td>201/500/400</td>
    </tr>
    <tr>
      <td>响应有效负载</td>
      <td><pre>{
    "data": {
        "templateId": “templateId”
    },
    "errors": []
}</pre></td>
    </tr>
  </tbody>
</table>

## <a name="view-the-scheduled-reports"></a>查看计划报告

使用此方法可以查看计划报告的列表。

<table>
  <thead>
    <tr>
      <th>项目</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Get</td>
      <td><pre>https://manage.devcenter.microsoft.com/analytics/driver/report</pre></td>
    </tr>
    <tr>
      <td>有效负载</td>
      <td>无</td>
    </tr>
    <tr>
      <td>响应代码</td>
      <td>201/500/400</td>
    </tr>
    <tr>
      <td>示例响应有效负载</td>
      <td><pre>{
    "data": [
        {
            "reportId": 2,
            "templateId": 7,
            "schedule": "{report details}",
            "isActive": true,
            "createdDatetime": "2018-06-24T17:04:18.487",
            "modifiedDatetime": "2018-06-25T08:28:42.063"
        },

                  {
            "reportId": 4,
            "templateId": 12,
            "schedule": "{report details}",
            "isActive": true,
            "createdDatetime": "2018-06-28T10:11:44.873",
            "modifiedDatetime": "2018-06-28T10:30:27.93"
        }
           ],
    "errors": []
}
</pre></td>
    </tr>
  </tbody>
</table>

## <a name="edit-a-scheduled-report"></a>编辑计划报告

使用此方法可以编辑现有计划报告。

<table>
  <thead>
    <tr>
      <th>项目</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>POST</td>
      <td><pre>https://manage.devcenter.microsoft.com/analytics/driver/report/{reportId}</pre></td>
    </tr>
    <tr>
      <td>有效负载</td>
      <td><pre>{
   "templateId":&lt;templateid&gt;,
   "Schedule":{
      "StartTime":"2018-07-24T00:00:00Z", //Datetime in UTC
      "RecurrenceInterval":12, // in hours
      "Recurrence":2
   }
}</pre></td>
    </tr>
    <tr>
      <td>响应代码</td>
      <td>201/500/400</td>
    </tr>
    <tr>
      <td>响应有效负载</td>
      <td><pre>{
    "data": {
        "reportId": &lt;reportId&gt;
    },
    "errors": []
}</pre></td>
    </tr>
  </tbody>
</table>

## <a name="pause-a-report"></a>暂停报告

使用此方法可以暂停计划报告。

<table>
  <tbody>
    <tr>
      <td>POST</td>
      <td><pre>https://manage.devcenter.microsoft.com/analytics/driver/report/pause/{reportId}</pre></td>
    </tr>
    <tr>
      <td>响应代码</td>
      <td>201/500/400</td>
    </tr>
    <tr>
      <td>响应有效负载</td>
      <td><pre>{
    "data": {
        "reportId": &lt;reportId&gt;
    },
    "errors": []
}</pre></td>
    </tr>
  </tbody>
</table>

## <a name="resume-a-report"></a>恢复报告

使用此方法可以恢复计划报告。

<table>
  <tbody>
    <tr>
      <td>POST</td>
      <td><pre>https://manage.devcenter.microsoft.com/analytics/driver/report/resume/{reportId}</pre></td>
    </tr>
    <tr>
      <td>响应代码</td>
      <td>201/500/400</td>
    </tr>
    <tr>
      <td>响应有效负载</td>
      <td><pre>{
    "data": {
        "reportId": &lt;reportId&gt;
    },
    "errors": []
}</pre></td>
    </tr>
  </tbody>
</table>

## <a name="see-also"></a>另请参阅

- [分析报告 API (Swagger)](https://apidocs.microsoft.com/services/analyticsreportingapis)

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
