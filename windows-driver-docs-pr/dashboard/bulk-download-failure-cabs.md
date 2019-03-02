---
title: 批量下载失败的 Cab
description: 使用作为获取报告数据 API 的一部分提供的报告检索 CabURL，然后下载失败的 cab。
ms.author: shganesh
ms.date: 09/01/2018
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 5afb3cf56642ec6a28827ee3d6df0afcd2b10874
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518512"
---
# <a name="bulk-download-failure-cabs"></a>批量下载失败的 Cab

使用此方法下载可用于特定失败哈希的所有失败 cab，从而使用从作为[获取报告数据](get-report-data.md) API 的一部分接收的报告中检索到的 failureHash 和 applicationId。

## <a name="request"></a>请求

### <a name="request-syntax"></a>请求语法

|方法|请求 URI|
|----|----|
|Get|`https://manage.devcenter.microsoft.com/v1.0/my/analytics/driver/cabdownloadbatch`|

## <a name="request-header"></a>请求标头

|标头|在任务栏的搜索框中键入|描述|
|----|----|----|
|授权|字符串|必需。 Azure AD 访问令牌的格式为 **Bearer** \<token\>。|

### <a name="request-parameters"></a>请求参数

|参数|在任务栏的搜索框中键入|描述|必需|
|----|----|----|----|
|applicationId|字符串|要为其检索错误数据的驱动程序的产品 ID 值。|是|
|failureHash|字符串|你希望获取详细信息的错误的唯一 ID。|是|
|startDate|日期|要检索的错误报告数据日期范围中的开始日期。 默认值为当前日期之前 30 天。|否|
|endDate|日期|要检索的错误报告数据日期范围中的结束日期。 默认值为当前日期。|否|
|top|int|要在请求中返回的数据行数。 如果未指定，最大值和默认值为 100。 当查询中存在多行数据时，响应正文中包含的下一个链接可用于请求下一页数据。|否|
|skip|int|要在查询中跳过的行数。 使用此参数可以浏览较大的数据集。 例如，top=100 和 skip=0，将检索前 100 行数据；top=100 和 skip=100，将检索之后的 100 行数据，依此类推。|否|

### <a name="request-example"></a>请求示例

以下示例演示了如何使用此方法获取 cabURI。

```json
GET https://manage.devcenter.microsoft.com/v1.0/my/analytics/driver/cabdownloadbatch?
applicationId=13984104677400476&failureHash=1fd83f6d-9fe0-96ec-2c47-ef08b65ccbed
HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

以下示例举例说明此请求的 JSON 响应正文。

```json
{
  "Value": [
      {
      "applicationId": "13984104677400476",
      "submissionId": "29989690_13984104677400476_1152921504626153337",
      "failureHash": "1fd83f6d-9fe0-96ec-2c47-ef08b65ccbed",
      "cabIdHash": "fb57b37b-d364-4caf-995b-d99ae651ee18",
      "cabUrl": "https://uswewatcab09.blob.core.windows.net/kernel-20170407/fb57b37b-d364-4caf-995b-d99ae651ee18.ext.zip?sv=2015-07-08&sr=b&sig=lRVFxW%2F7GlumJHas0QxX5%2Bnvkrdi5lqijKQaGeB%2BUQA%3D&se=2017-04-28T02%3A37%3A28Z&sp=r",
      "date": "2017-04-07 13:53:43",
      "cabExpirationTime": "2017-05-07 13:53:43"
    },
    {
      "applicationId": "13984104677400476",
      "submissionId": "29989690_13984104677400476_1152921504626153337",
      "failureHash": "1fd83f6d-9fe0-96ec-2c47-ef08b65ccbed",
      "cabIdHash": "e261603b-1e86-4094-bca5-7ac4f8bf1aab",
      "cabUrl": "https://uswewatcab12.blob.core.windows.net/kernel-20170406/e261603b-1e86-4094-bca5-7ac4f8bf1aab.ext.zip?sv=2015-07-08&sr=b&sig=WCM3yNXJsIb1ME4hQICNGHBxSCWU%2FPq7ykCGNrd3lNo%3D&se=2017-04-28T02%3A37%3A28Z&sp=r",
      "date": "2017-04-07 06:17:01",
      "cabExpirationTime": "2017-05-07 06:17:01"
    }]
}
```

## <a name="see-also"></a>另请参阅

- [分析报告 API (Swagger)](https://apidocs.microsoft.com/services/analyticsreportingapis)

- [下载失败的 Cab](download-failure-cabs.md)
