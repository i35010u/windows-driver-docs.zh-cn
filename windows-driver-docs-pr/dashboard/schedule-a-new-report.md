---
title: 计划新报告
description: 如何基于 Microsoft 硬件开发中心的报告模板计划自定义错误报告。
ms.topic: article
ms.author: shganesh
ms.date: 09/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5d7aa593bee432cb9a3732c8e0298af06e2f9ca0
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63337112"
---
# <a name="schedule-a-new-report"></a>计划新报告

成功创建报告模板并收到 templateID  后，请使用此方法设置频率并计划定期发送给你的报告。

## <a name="request-syntax"></a>请求语法

|方法|请求 URI|
|----|----|
|POST|`https://manage.devcenter.microsoft.com/analytics/driver/report`|

## <a name="request-header"></a>请求头

|标头|在任务栏的搜索框中键入|描述|
|----|----|----|
|授权|字符串|必需。 采用 **Bearer** \<令牌\> 格式的 Azure AD 访问令牌 |
|内容类型|字符串|Application/JSON|

## <a name="sample-request-payload"></a>示例请求有效负载

使用以下格式定义需要运行自定义报告的计划：

```json
{
  "templateId": 15, // sample report template id
  "schedule":
    {
      "startTime": "2018-07-24T00:00:00Z",//Date Time in UTC
      "recurrenceInterval": 12, // in hours
      "recurrence": 10    // number of times you want the report to run
    }
  
}
```

## <a name="parameters"></a>参数

此表包含计划报告 JSON 中的参数说明。

<table>
    <thead>
        <tr>
            <th>参数</th>
            <th>必需</th>
           <th>描述</th>
        </tr>
    </thead>
    <tbody>
       <tr>
          <td>templateId</td>
          <td>是</td>
          <td>作为对创建报告模板 API 的响应而收到的 templateId 值</td>
        </tr>
        <tr>
            <td>startTime</td>
            <td>是</td>
            <td>需要首次运行报告的时间，格式如下：<pre>yyyy-MM-ddTHH:mm:ssZ</pre></td>
        </tr>
        <tr>
           <td>recurrenceInterval</td>
           <td>是</td>
           <td>以小时为单位的时间间隔，在此时间间隔之后，需要报告再次运行。 允许的最小时间间隔为 12 小时。</td>
        </tr>
        <tr>
            <td>重复次数</td>
            <td>是</td>
            <td>需要此报告运行的次数。</td>
        </tr>
        <tr>
           <td>CallbackURL</td>
           <td>否</td>
           <td>准备好报告数据后需要通知的 URL</td>
        </tr>

</tbody>
</table>

## <a name="response"></a>响应

响应有效负载的结构如下所示，采用 JSON 格式：

<table>
<thead>
    <tr>
      <th>项目</th>
      <th>描述</th>
    </tr>
</thead>
    <tr>
      <td>响应代码</td>
      <td>201/500/400</td>
    </tr>
    <tr>
      <td>响应有效负载</td>
      <td><pre>{
    "data": {
        "reportId": reportId
    },
    "errors": []
}
</pre>
      </td>
    </tr>
<tr></tr>
  </tbody>
</table>

## <a name="response-parameters"></a>响应参数

下表介绍响应中的参数。  

|参数|描述|
|----|----|
|reportId|表示计划报告的 ID|

如果设置了回调 URL 以在报告数据准备好时收到通知，则可以在报告数据可供下载后立即调用[获取报告数据](get-report-data.md)方法提取报告数据。

## <a name="see-also"></a>另请参阅

- [分析报告 API (Swagger)](https://apidocs.microsoft.com/services/analyticsreportingapis)

- [获取报告数据](get-report-data.md)

- [管理报告模板](manage-report-templates-and-scheduled-reports.md)

- [示例报告模板](sample-report-templates.md)

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
