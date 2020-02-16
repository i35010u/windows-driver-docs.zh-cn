---
title: 获取产品
description: Microsoft 硬件 API 中的此方法可检索注册到 Windows 开发人员中心帐户的特定产品的数据。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 349dcb2238ba7dedf71f28c8bf02cea57a770516
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072216"
---
# <a name="get-a-product"></a>获取一个产品

在 Microsoft 硬件 API 中使用此方法可检索注册到 Windows 开发人员中心帐户的特定产品的数据。

## <a name="prerequisites"></a>必备条件

完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)（如果尚未这样做），然后尝试使用这其中的任何方法。

## <a name="request"></a>请求

此方法具有以下语法。 请参阅以下部分，获取标头和请求正文的使用示例和描述。

|方法|请求 URI|
|:--|:--|
|GET|https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}|

### <a name="request-header"></a>请求头

| Header | 类型 | 说明 |
|:--|:--|:--|
| 授权 | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** \<token\>。 |
| accept | 字符串 | 可选。 指定内容的类型。 允许的值是“application/json” |


### <a name="request-parameters"></a>请求参数

请勿为此方法提供请求参数

### <a name="request-body"></a>请求正文

请勿为此方法提供请求正文。

### <a name="request-examples"></a>请求示例

以下示例演示了如何检索注册到帐户的特定产品的相关信息。

```cpp
GET https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14039471039847257 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

以下示例演示了注册到开发者帐户的特定产品的成功请求所返回的 JSON 响应正文。 有关响应正文中这些值的详细信息，请参阅以下部分。

```json
{
    "id": 9007199267351834,
    "sharedProductId": 1152921504606971255,
    "links": [
        {
            "href": "https://hardwareapi.microsoft.com/api/v1/hardware/products/9007199267351834",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://hardwareapi.microsoft.com/api/v1/hardware/products/9007199267351834/submissions",
            "rel": "get_submissions",
            "method": "GET"
        }
    ],
    "isCommitted": true,
    "isExtensionInf": false,
    "originType": "author",
    "sourceProductId": 0,
    "sourcePublisherId": 0,
    "isRetpolineCompiled": false,
    "message": "",
    "deviceMetadataIds": [],
    "deviceType": "notSet",
    "isTestSign": false,
    "isFlightSign": false,
    "marketingNames": [],
    "productName": "NewDriverHacked",
    "selectedProductTypes": {},
    "requestedSignatures": [
        "WINDOWS_v100_X64_TH1_FULL",
        "WINDOWS_v63_X64"
    ],
    "additionalAttributes": {},
    "testHarness": "hlk"
}
```

## <a name="error-codes"></a>错误代码

有关详细信息，请参阅[错误代码](get-product-data.md#error-codes)。

## <a name="see-also"></a>另请参阅

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
