---
title: 获取所有提交
description: Microsoft 硬件 API 中的此方法会检索产品的所有提交的数据。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: aad98eb7801aec7062ea2cc670fa779298e04617
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072200"
---
# <a name="get-all-submissions"></a>获取所有提交

使用 Microsoft 硬件 API 中的此方法可检索产品的所有提交的数据。

## <a name="prerequisites"></a>必备条件

完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)（如果尚未这样做），然后尝试使用这其中的任何方法。

## <a name="request"></a>请求

此方法具有以下语法。 请参阅以下部分，获取标头和请求正文的使用示例和描述。

|方法|请求 URI|
|:--|:--|
|GET| `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions` |

### <a name="request-header"></a>请求头

|Header|类型|说明
|:--|:--|:--|
|Authorization|字符串|必需。 Azure AD 访问令牌的格式为 **Bearer** \<token\>。|
|accept|字符串|可选。 指定内容的类型。 允许的值是“application/json”|

### <a name="request-parameters"></a>请求参数

请勿为此方法提供请求参数。

### <a name="request-body"></a>请求正文

请勿为此方法提供请求正文。

### <a name="request-examples"></a>请求示例

以下示例演示了如何检索有关产品的所有提交的信息。


```cpp
GET https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

以下示例演示了所有产品提交的成功请求所返回的 JSON 响应正文。 为了简洁起见，此示例仅显示该请求返回的前两个提交的数据。 有关响应正文中这些值的详细信息，请参阅以下部分。

```json
{
  "value": [
    {
      "id": 1152921504621442000,
      "productId": 13635057453741328,
      "links": [
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions/1152921504621441944",
          "rel": "self",
          "method": "GET"
        },
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions/1152921504621441944",
          "rel": "update_submission",
          "method": "PATCH"
        }
      ],
      "isExtensionInf": true,
      "isUniversal": true,
      "isDeclarativeInf": true,
      "name": "HARRY-Duatest2",
      "type": "derived"
    },
    {
      "id": 1152921504621442000,
      "productId": 13635057453741328,
      "workflowStatus": {
        "currentStep": "finalizeIngestion",
        "state": "completed",
        "messages": []
      },
      "links": [
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions/1152921504621441946",
          "rel": "self",
          "method": "GET"
        },
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions/1152921504621441946",
          "rel": "update_submission",
          "method": "PATCH"
        }
      ],
      "isExtensionInf": true,
      "isUniversal": true,
      "isDeclarativeInf": true,
      "name": "updated-1",
      "type": "derived"
    },
    {
      "id": 1152921504621442000,
      "productId": 13635057453741328,
      "workflowStatus": {
        "currentStep": "finalizeIngestion",
        "state": "completed",
        "messages": []
      },
      "links": [
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions/1152921504621441930",
          "rel": "self",
          "method": "GET"
        },
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions/1152921504621441930",
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
  ],
  "links": [
    {
      "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions",
      "rel": "self",
      "method": "GET"
    }
  ]
}
```

### <a name="response-body"></a>响应正文

|值|类型|说明|
|:--|:--|:--|
|value|数组|一个对象数组，其中包含有关产品的每个提交的信息。 有关每个对象中的数据的详细信息，请参阅[提交资源](get-product-data.md#submission-resource)。|
|链接|数组|一个对象数组，其中包含有关包含实体的有用链接。 有关更多详细信息，请参阅[链接对象](get-product-data.md#link-object)|

## <a name="error-codes"></a>错误代码

有关详细信息，请参阅[错误代码](get-product-data.md#error-codes)。

## <a name="see-also"></a>另请参阅

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
