---
title: 创建新产品
description: 在 Microsoft 硬件 API 中使用此方法创建新的硬件产品。
ms.date: 04/05/2018
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 69bea184cab181b3a92713957d7a643a6164df11
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072182"
---
# <a name="create-a-new-product"></a>创建新产品

在 Microsoft 硬件 API 中使用此方法创建新的硬件产品。

## <a name="prerequisites"></a>必备条件

完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)（如果尚未这样做），然后尝试使用这其中的任何方法。

## <a name="request"></a>请求

此方法具有以下语法。 请参阅以下部分，获取标头和请求正文的使用示例和描述。

| 方法 | 请求 URI |
|:--|:--|
| POST | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products` |


### <a name="request-header"></a>请求头

| Header | 类型 | 说明 |
|:--|:--|:--|
| Authorization | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** \<token\>。 |
| accept | 字符串 | 可选。 指定内容的类型。 允许的值是“application/json” |


### <a name="request-parameters"></a>请求参数

请勿为此方法提供请求参数。

### <a name="request-body"></a>请求正文

以下示例演示了用于创建新产品的 JSON 请求正文。 有关请求正文中的值的详细信息，请参阅 json 下面的表。

```json
{
  "productName": "Test_Network_Product2-R",
  "testHarness": "Attestation",
  "announcementDate": "2018-01-01T00:00:00",
  "deviceMetadataIds": [],
  "firmwareVersion": "980",
  "deviceType": "external",
  "isTestSign": false,
  "isFlightSign": false,  
  "marketingNames": [],
  "productName": "VST_apdevtest1",
  "selectedProductTypes": {
    "windows_v100_RS3": "Unclassified"
  },
  "requestedSignatures": [
    "WINDOWS_v100_RS3_FULL",
    "WINDOWS_v100_X64_RS3_FULL",
    "WINDOWS_VISTA"
  ],
  "additionalAttributes": {},
  "packageType": "HLK"
}
```

有关请求中的字段的详细信息，请参阅[产品资源](get-product-data.md#product-resource)。

### <a name="request-examples"></a>请求示例

以下示例演示了如何创建新产品。

```cpp
POST https://manage.devcenter.microsoft.com/v2.0/my/hardware/products HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

以下示例演示了创建产品的成功请求所返回的 JSON 响应正文。 有关响应正文中这些值的详细信息，请参阅以下部分。

```json
{
  "id": 14631253285588838,
  "sharedProductId": 1152921504607010608,
  "links": [
    {
      "href": "https:// manage.devcenter.microsoft.com/api/v1/hardware/products/14631253285588838",
      "rel": "self",
      "method": "GET"
    },
    {
      "href": "https:// manage.devcenter.microsoft.com/api/v1/hardware/products/14631253285588838/submissions",
      "rel": "get_submissions",
      "method": "GET"
    }
  ],
  "isCommitted": false,
  "isExtensionInf": false,
  "announcementDate": "2018-01-01T00:00:00",
  "deviceMetadataIds": [],
  "firmwareVersion": "980",
  "deviceType": "external",
  "isTestSign": false,
  "isFlightSign": false,  
  "marketingNames": [],
  "productName": "VST_apdevtest1",
  "selectedProductTypes": {
    "windows_v100_RS3": "Unclassified"
  },
  "requestedSignatures": [
    "WINDOWS_v100_RS3_FULL",
    "WINDOWS_v100_X64_RS3_FULL",
    "WINDOWS_VISTA"
  ],
  "additionalAttributes": {},
  "testHarness": "attestation"
}
```

### <a name="response-body"></a>响应正文

有关更多详细信息，请参阅[产品资源](get-product-data.md#product-resource)

## <a name="error-codes"></a>错误代码

有关详细信息，请参阅[错误代码](get-product-data.md#error-codes)。

## <a name="see-also"></a>另请参阅

[硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
