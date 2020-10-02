---
title: 为产品创建新的提交
description: 在 Microsoft 硬件 API 中使用此方法为产品创建新的提交。
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9c53188a3fc73810f09f8d8c4307fa7d75b2fcb9
ms.sourcegitcommit: acef3c512676aad3aed1934cbe3d0f16e6d37619
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "91372886"
---
# <a name="create-a-new-submission-for-a-product"></a>为产品创建新的提交

在 Microsoft 硬件 API 中使用此方法为产品创建新的提交。 使用此方法之前，请确保已创建了新产品。 有关详细信息，请参阅[创建新产品](create-a-new-product.md)。

## <a name="prerequisites"></a>必备条件

完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)（如果尚未这样做），然后尝试使用这其中的任何方法。

## <a name="request"></a>请求

此方法具有以下语法。 请参阅以下部分，获取标头和请求正文的使用示例和描述。

| 方法 | 请求 URI |
|:--|:--|
| POST | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions` |


此方法中的 productId 是提交所适用于的产品。

### <a name="request-header"></a>请求头

| Header | 类型 | 说明 |
|:--|:--|:--|
| Authorization | 字符串 | 必需。 Azure AD 访问令牌的格式为 Bearer \<token\>。 |
| 接受 | 字符串 | 可选。 指定内容的类型。 允许的值是“application/json” |


### <a name="request-parameters"></a>请求参数

请勿为此方法提供请求参数。

### <a name="request-body"></a>请求正文

以下示例演示了用于创建新提交的 JSON 请求正文。

```json
{
  "name": "VST_apdevtest1_init",
  "type": "initial"
}
```

有关请求中的字段的详细信息，请参阅[提交资源](get-product-data.md#submission-resource)。

### <a name="request-examples"></a>请求示例

以下示例演示如何创建新提交。

```cpp
POST https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14631253285588838/submissions HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

以下示例演示了为产品创建新提交的成功请求所返回的 JSON 响应正文。 有关响应正文中这些值的详细信息，请参阅以下部分。

```json
{
  "id": 1152921504621465124,
  "productId": 14631253285588838,
  "downloads": {
    "items": [
      {
        "type": "initialPackage",
        "url": "https://ingestionpackages.blob.core.windows.net/ingestion/38c19eaf-7377-4834-893c-28d5791f7896?sv=2017-04-17&sr=b&sig=SlD5j5e067oA4Y3hdk1sPW3UycTSUVlIp80WbWvj4A8%3D&se=2018-03-20T05:00:14Z&sp=rwl"
      }
    ],
    "messages": []
  },
  "links": [
    {
      "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14631253285588838/submissions/1152921504621465124",
      "rel": "self",
      "method": "GET"
    },
    {
      "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14631253285588838/submissions/1152921504621465124",
      "rel": "update_submission",
      "method": "PATCH"
    }
  ],
  "commitStatus": "commitPending",
  "isExtensionInf": true,
  "isUniversal": true,
  "isDeclarativeInf": true,
  "name": "VST_apdevtest1_init",
  "type": "initial"
}
```

### <a name="response-body"></a>响应正文

有关更多详细信息，请参阅[提交资源](get-product-data.md#submission-resource)。

## <a name="error-codes"></a>错误代码

有关详细信息，请参阅[错误代码](get-product-data.md#error-codes)。

## <a name="see-also"></a>另请参阅

[硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
