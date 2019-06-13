---
title: 创建新的报告模板
description: 介绍如何创建新的报告模板用于生成驱动程序故障报告。 包括 REST API 信息。
ms.author: shganesh
ms.topic: article
ms.date: 09/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: a928f221eef74eaec6a869729b8b0d930cc17e18
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63337422"
---
# <a name="create-a-new-report-template"></a>创建新的报告模板

使用此方法可根据业务需求创建新的报告模板。 可以使用[管理报告模板和计划的报告](manage-report-templates-and-scheduled-reports.md)中所列的方法管理现有的报告模板

## <a name="request-syntax"></a>请求语法

|方法|请求 URI|
|----|----|
|POST|`https://manage.devcenter.microsoft.com/analytics/driver/reporttemplate`|

## <a name="request-header"></a>请求头

|标头|在任务栏的搜索框中键入|描述|
|----|----|----|
|授权|字符串|必需。 采用 **Bearer** \<令牌\> 格式的 Azure AD 访问令牌 |
|内容类型|字符串|Application/JSON|

## <a name="request-payload"></a>请求有效负载

按如下所示以 JSON 格式定义报告模板。

```json
{
  "view": " IHVDriver", // select “OEMDriver” for OEM Hardware Error data

  "projection": [
    "column1",
    "column2",
    "column3"
  ],

  "dateRange":
    {
      "reportPeriod": "Yesterday" // select date range
    }
  ,

  "condition": {
    "and": [
      {
        "attribute": "column1",
        "operator": "eq",
        "value": "1" // value that you desire to compare
      },
      {
        "condition": {
          "or": [
            {
              "attribute": "column2",
              "operator": "eq",
              "value": "2" //value that you desire to compare
            },
            {
              "attribute": "column3",
              "operator": "eq",
              "value": "3" //value that you desire to compare
            }
          ]
        }
      }
    ],

    "or": []
  },

  "aggregation": {
    "aggregatedColumns": [
      "SUM(column1)",
      "DCOUNT(column2)"
    ],

    "condition": {
      "or": [
        {
          "attribute": "column5",
          "operator": "gt",
          "value": "100" //value that you desire to compare
        }
      ]
    }
  },

  "orderby": [
    {
      "attribute": "column4",
      "sort": "desc"
    }
  ],

  "limit": 100
}
```

## <a name="parameters"></a>参数

下表描述了报告模板创建 JSON 中的参数。

<table>
    <thead>
      <tr>
            <th>参数</th>
            <th>必需</th>
            <th>描述</th>
            <th>允许的值</th>
        </tr>
    </thead>
    <tbody>
    <tr>
        <td>视图</td>
        <td>是</td>
        <td>如果你是 IHV/ISV 并想要生成驱动程序故障报告，请选择“IHVDriver”。<b></b><br/>如果你是 OEM 合作伙伴并想要生成硬件故障报告，请选择“OEMDriver”。<b></b></td>
        <td><b>IHVDriver</b> <br/><b>OEMDriver</b></td>
    <tr/>
    <tr>
        <td>projection</td>
        <td>是</td>
        <td>报告中所需的列列表。 此参数的值根据视图是“IHVDriver”还是“OEMDriver”而有所不同<b></b><b><b> </td>
        <td>下面是可用的列列表</td>
    </tr>
    <tr>
        <td>reportPeriod</td>
        <td>是</td>
        <td>请求故障数据的日期范围</td>
        <td>昨天<br/>Last3Days<br/>Last7Days<br/>Last10Days<br/>Last15Days<br/>Last30Days<br/>Last60Days<br/>Last90Days</td>
    </tr>
    <tr>
        <td>操作员</td>
        <td>否</td>
        <td>筛选条件支持的运算符集</td>
        <td>IN<br/>EQ<br/>NEQ<br/>LT<br/><br/>GT<br/>LTE<br/>GTE<br/>LIKE</td>
    </tr>
    <tr>
        <td>aggregatedColumns</td>
        <td>否</td>
        <td>错误数据支持的聚合集</td>
        <td>SUM<br/>AVG<br/>COUNT<br/>DCOUNT<br/>MAX<br/>MIN</td>
    </tr>
    <tr>
        <td>orderby 属性</td>
        <td>否</td>
        <td>定义结果集的顺序 - 允许按 asc（升序）或 desc（降序）排序</td>
        <td>支持所有可用列 </td>
    </tr>
    <tr>
        <td>limit</td>
        <td>否</td>
        <td>限制响应中的行数</td>
        <td>整数 &gt;=0<br/>0 表示所有记录</td>
    </tr>
    </tbody>
</table>

## <a name="response"></a>响应

响应有效负载的结构如下所示，采用 JSON 格式。

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
        <td>201/500/400</td>
      </tr>
      <tr>
      <td>响应有效负载</td>
          <td><pre>{
    "data": {
        "templateId": templateId
  },
  "errors": null  }</pre></td>
      </tr>
     </tbody>
</table>

## <a name="response-parameters"></a>响应参数

下表包含响应中的参数说明。

|参数|描述|
|----|----|
|templateId|这是创建的报告模板的模板 ID。 用作计划报告 API 的输入。 有关详细信息，请参阅[计划新报告](schedule-a-new-report.md)。

可以使用[管理报告模板和计划的报告](manage-report-templates-and-scheduled-reports.md)中所示的方法管理现有的报告。 可以在[示例报告模板](sample-report-templates.md)中找到示例报告模板的列表。

## <a name="columns-available-for-projection-ihv-and-oem-view"></a>可用于投影的列（IHV 和 OEM 视图）

可以在适用于 IHV 或 ISV 的 Windows 10、Windows 8.x 和 Windows 7 驱动程序报告中选择以下列。

<table>
  <thead>
    <tr>
      <th>列名称</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ReportId</td>
      <td>包含此记录的报告的报告 ID</td>
    </tr>
    <tr>
      <td>FailureDate</td>
      <td>发生故障的日期，采用 mmddyy 格式</td>
    </tr>
    <tr>
      <td>FailureDateTime</td>
      <td>发生故障时的时间戳</td>
    </tr>
    <tr>
      <td>ApplicationId</td>
      <td>（仅在“IHVDriver”视图中可用）发生故障的驱动程序提交内容的应用程序 ID 或专用产品 ID<i></i></td>
    </tr>
    <tr>
      <td>SubmissionId</td>
      <td>（仅在“IHVDriver”视图中可用）发生故障的驱动程序的提交 ID<i></i></td>
    </tr>
    <tr>
      <td>FailureName</td>
      <td>故障桶的名称</td>
    </tr>
    <tr>
      <td>FailureHash</td>
      <td>故障桶的故障哈希值</td>
    </tr>
    <tr>
      <td>符号</td>
      <td>故障的符号（如果有）</td>
    </tr>
    <tr>
      <td>OSVersion</td>
      <td>发生故障的操作系统的版本</td>
    </tr>
    <tr>
      <td>OSName</td>
      <td>（仅在“IHVDriver”视图中可用）- 发生故障的操作系统的友好名称<i></i></td>
    </tr>
    <tr>
      <td>EventType</td>
      <td>指示故障事件是系统故障事件还是内核故障事件</td>
    </tr>
    <tr>
      <td>市场</td>
      <td>发生故障的市场</td>
    </tr>
    <tr>
      <td>DeviceType</td>
      <td>发生故障的设备类型</td>
    </tr>
    <tr>
      <td>DriverName</td>
      <td>导致故障的驱动程序的名称</td>
    </tr>
    <tr>
      <td>DriverVersion</td>
      <td>导致故障的驱动程序的版本</td>
    </tr>
    <tr>
      <td>体系结构</td>
      <td>发生故障的体系结构</td>
    </tr>
    <tr>
      <td>OEMName</td>
      <td>（仅在“IHVDriver”视图中可用）- 发生故障的 OEM 的名称<i></i></td>
    </tr>
    <tr>
      <td>OEMModel/Model</td>
      <td>发生故障的 OEM 型号的名称<br/>在“IHVDriver”视图中名为“OEMModel”<i></i><i></i><br/>在“OEMDriver”视图中名为“Model”<i></i><i></i>
</td>
    </tr>
    <tr>
      <td>FlightRing</td>
      <td>发生故障的外部测试环</td>
      </tr>
    <tr>
      <td>模式</td>
      <td>指示故障是在内核模式还是用户模式下发生的</td>
    </tr>
    <tr>
      <td>CPUName</td>
      <td>发生崩溃的设备的 CPU 名称</td>
    </tr>
    <tr>
      <td>OSSKUType</td>
      <td>发生故障的 OS SKU 的名称</td>
    </tr>
    <tr>
      <td>ReleaseName</td>
      <td>发生故障的 OS 的 OS 版本名称</td>
    </tr>
    <tr>
      <td>Baseboard</td>
      <td>（仅在“OEMDriver”视图中可用）指示发生故障的主板<i></i></td>
    </tr>
    <tr>
      <td>ModelFamily</td>
      <td>（仅在“OEMDriver”视图中可用）指示发生故障的型号系列<i></i></td>
    </tr>
    <tr>
      <td>CabType</td>
      <td>指示可用的 cab 是内核 cab、MINI cab 还是 FULL cab</td>
    </tr>
    <tr>
      <td>CabIdHash</td>
      <td>可用于通过 <a href="https://manage.devcenter.microsoft.com/v1.0/my/analytics/driver/cabdownload" data-raw-source="[CabDownload](https://manage.devcenter.microsoft.com/v1.0/my/analytics/driver/cabdownload)">CabDownload</a> API 下载 cab 文件的 CabID 的哈希</td>
    </tr>
    <tr>
      <td>DeviceId</td>
      <td>发生故障的设备 ID</td>
    </tr>
    <tr>
      <td>HardwareId</td>
      <td>发生故障的设备的硬件 ID</td>
    </tr>
    <tr>
      <td>CabCollectionTime</td>
      <td>Microsoft 服务器收集 cab 时的时间戳</td>
    </tr>
    <tr>
      <td>CabExpirationTime</td>
      <td>cab 过期且不再可供下载的时间</td>
    </tr>
    <tr>
      <td>EventCount</td>
      <td>该故障哈希发生的故障事件数</td>
    </tr>
  </tbody>
</table>

可以使用[管理报告模板和计划的报告](manage-report-templates-and-scheduled-reports.md)中所示的方法管理现有的报告。 可以在[示例报告模板](sample-report-templates.md)中找到示例报告模板的列表。

## <a name="see-also"></a>另请参阅

- [分析报告 API (Swagger)](https://apidocs.microsoft.com/services/analyticsreportingapis)

- [计划新报告](schedule-a-new-report.md)

- [管理报告模板](manage-report-templates-and-scheduled-reports.md)

- [示例报告模板](sample-report-templates.md)

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
