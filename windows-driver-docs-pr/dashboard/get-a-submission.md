---
title: ''
description: ''
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3d65e4bae3389d86051a2ee9f80c5043716ddac9
ms.sourcegitcommit: a70dcf63a439d278ae0194733d9fa2adfe496c89
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66813569"
---
# <a name="get-a-submission"></a>获取提交

使用 Microsoft 硬件 API 中的此方法可检索产品的特定提交的数据。

## <a name="prerequisites"></a>系统必备

如果尚未开始操作，请先完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)，然后再尝试使用其中任何方法。

## <a name="request"></a>请求

此方法具有以下语法。 请参阅以下部分，获取标头和请求正文的使用示例和描述。

|方法|请求 URI|
|:--|:--|
|GET|`https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productID}/submissions/{submissionID}` |

### <a name="request-header"></a>请求头

|Header|在任务栏的搜索框中键入|描述|
|:--|:--|:--|
|授权|string|必需。 Azure AD 访问令牌的格式为 **Bearer** \<token\>。|
|accept|string|可选。 指定内容的类型。 允许的值是“application/json”|

### <a name="request-parameters"></a>请求参数

请勿为此方法提供请求参数。

### <a name="request-body"></a>请求正文

请勿为此方法提供请求正文。

### <a name="request-examples"></a>请求示例

以下示例演示了如何检索有关产品的所有提交的信息。


```cpp
GET https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/13635057453741329/submissions/1152921504621441930 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

以下示例演示了特定产品提交的成功请求所返回的 JSON 响应正文。 有关响应正文中这些值的详细信息，请参阅以下部分。

```json
{
  "id": 1152921504621442000,
  "productId": 13635057453741328,
  "workflowStatus": {
    "currentStep": "finalizeIngestion",
    "state": "completed",
    "messages": []
  },
  "downloads": {
    "items": [
      {
        "type": "initialPackage",
        "url": "https://ingestionpackages.blob.core.windows.net/ingestion/dc55b8c6-a01c-40b6-b815-cac8bc08812a?sv=2016-05-31&sr=b&sig=ipjW3RsVC75lZrcEZRh9JmTX89L4gTIKkxwqv9F8Axs%3D&se=2018-03-12T15:32:10Z&sp=rl"
      },
      {
        "type": "derivedPackage",
        "url": "https://ingestionpackages.blob.core.windows.net/ingestion/6bd77dbf-a851-46d2-b703-29ea4efae006?sv=2016-05-31&sr=b&sig=O5XQf%2FzMbI2FFt5WwSUJWL1JbWY4JXXPRkCKAnX7IRs%3D&se=2018-03-12T15:32:10Z&sp=rl&rscd=attachment%3B filename%3DShell_1152921504621441930.hlkx"
      },
      {
        "type": "signedPackage",
        "url": "https://ingestionpackages.blob.core.windows.net/ingestion/0b83a294-c1d1-4136-82a1-dd52f51841e3?sv=2016-05-31&sr=b&sig=zTfxKJmaTwpbFol%2FpAKG0QuXJTTxm5aZ0F2wQQI8whc%3D&se=2018-03-12T15:32:10Z&sp=rl"
      },
      {
        "type": "certificationReport",
        "url": "https:// manage.devcenter.microsoft.com/dashboard/hardware/Driver/DownloadCertificationReport/29963920/13635057453741329/1152921504621441930"
      }
    ],
    "messages": []
  },
  "links": [
    {
      "href": "https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/13635057453741329/submissions/1152921504621441930",
      "rel": "self",
      "method": "GET"
    },
    {
      "href": "https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/13635057453741329/submissions/1152921504621441930",
      "rel": "update_submission",
      "method": "PATCH"
    }
  ],
  "isExtensionInf": true,
  "isUniversal": true,
  "isDeclarativeInf": true,
  "name": "HARRY-Duatest2",
  "type": "initial"
}
```

### <a name="response-body"></a>响应正文

有关更多详细信息，请参阅[提交资源](get-product-data.md#submission-resource)

## <a name="error-codes"></a>错误代码

有关详细信息，请参阅[错误代码](get-product-data.md#error-codes)。

## <a name="see-also"></a>请参阅

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
