---
title: 获取报告数据
description: 查询 Windows 驱动程序提交失败报告的状态并获取失败详细信息报告。
ms.author: shganesh
ms.topic: article
ms.date: 09/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3b3398095214950fe214ac72229330e1c575e980
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518546"
---
# <a name="get-report-data"></a>获取报告数据

通过此方法可以使用 reportId 查询报告的状态并获取失败详细信息报告。 如果准备就绪，此方法会返回报告下载链接，否则会返回状态。

## <a name="request-syntax"></a>请求语法

|方法|请求 URI|
|----|----|
|GET|`https://manage.devcenter.microsoft.com/analytics/driver/reportdata/{reportId}?startDate={yyyy-mm-dd}&endDate={yyyy-mm-dd}`|

## <a name="request-header"></a>请求头

|标头|在任务栏的搜索框中键入|描述|
|----|----|----|
|授权|字符串|必需。 Azure AD 访问令牌的格式为 **Bearer** \<token\>|
|内容类型|字符串|Application/JSON|

## <a name="parameters"></a>参数

下表介绍了获取失败详细信息 API 中的参数。

|参数|描述|
|----|----|
|reportId|调用[计划报告 API](schedule-a-new-report.md) 时收到的报告的 reportId|
|startDate|请求生成报告的开始日期（格式为 `yyyy-mm-dd`）|
|endDate|请求生成报告的结束日期（格式为 `yyyy-mm-dd`）|

## <a name="response"></a>响应

响应有效负载的结构是一个值数组，如下表所示。

<table>
  <thead>
    <tr>
      <th>项目</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>响应代码</td>
      <td>200/500/400</td>
    </tr>
    <tr>
      <td>响应有效负载</td>
      <td><pre>{
    "data": [
        {
            "ReportDatetime": "2018-01-20T05:35:32",
            "ReportStatus": "Completed",
            "ReportLocation": "https://hardwareanalyticsint.blob.core.windows.net/drivers/Reports/2.txt?sv=2017 .... "
        },
        {
            "ReportDatetime": "2018-01-23T05:35:32",
            "ReportStatus": "Failed",
            "ReportLocation": ""
        }
    ],
    "errors": []
}</pre></td>
    </tr>
  </tbody>
</table>

## <a name="response-parameters"></a>响应参数

下表介绍了响应中的参数。

|参数|描述|
|----|----|
|ReportDatetime|运行报告的日期|
|ReportStatus|ReportDateTime 相关报告的状态。 值可以为“Completed”、“Pending”、“In Progress”、“Failed”。|
|ReportLocation|如果 ReportStatus 返回“Completed”，则为报告的下载链接|

> [!NOTE]
> ReportLocation 链接将在 12 小时后过期。 如果未在 12 小时时间窗口内下载数据，则必须使用“获取报告数据”API 获取新的报告链接。

可以使用[管理报告模板和计划报告](manage-report-templates-and-scheduled-reports.md)中所述的方法管理报告模板。

## <a name="see-also"></a>另请参阅

- [分析报告 API (Swagger)](https://apidocs.microsoft.com/services/analyticsreportingapis)

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
