---
title: 获取发货标签
description: Microsoft 硬件 API 中的这些方法可获取注册到硬件开发人员中心帐户的硬件产品的发货标签。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: 2b34be22c944b18f0c519941881dea2d7727d4b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518406"
---
# <a name="get-a-shipping-label"></a>获取发货标签

使用此方法可检索特定产品提交的特定发货标签的数据。

## <a name="prerequisites"></a>必备条件

如果尚未开始操作，请先完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)，然后再尝试使用其中任何方法。 在使用这些方法之前，产品和提交必须已存在于你的开发人员中心帐户中。 若要创建或管理产品提交，请参阅[管理产品提交](manage-product-submissions.md)中的方法。

## <a name="request"></a>请求

此方法具有以下语法。 请参阅以下部分，获取标头和请求正文的使用示例和描述。

|方法|请求 URI|
|--|--|
|GET|`https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productId}/submissions/{submissionId}/shippingLabels/{shippingLabelId}`|

### <a name="request-header"></a>请求头

| 标头 | 在任务栏的搜索框中键入 | 描述 |
|:--|:--|:--|
| 授权 | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** \*<token\>*。 |
| accept | 字符串 | 可选。 指定内容的类型。 允许的值是“application/json” |

### <a name="request-parameters"></a>请求参数

此方法的请求参数为可选项。

|名称|在任务栏的搜索框中键入|描述|
|:--|:--|:--|
| includeTargetingInfo | 布尔值 | 可选。 如果此参数设置为 true，则发货标签会返回发货标签的目标详细信息，例如硬件 ID 和 CHID。 有关详细信息，请参阅[目标对象](get-shipping-labels.md#targeting-object)。|

### <a name="request-body"></a>请求正文

请勿为此方法提供请求正文。

### <a name="request-examples"></a>请求示例

以下示例演示了如何检索注册到帐户的特定产品的相关信息。

```cpp
GET https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/14461751976964156/submissions/1152921504621467600/shippingLabels/1152921504606980300 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

以下示例演示了特定发货标签的成功请求所返回的 JSON 响应正文。 有关响应正文中的值的详细信息显示在示例后面的表中。

```json
{
  "id": 1152921504606978300,
  "productId": 14461751976964156,
  "submissionId": 1152921504621467600,
  "publishingSpecifications": {
    "goLiveDate": "2018-04-12T05:28:32.721Z",
    "visibleToAccounts": [
      27691110,
      27691111
    ],
    "isAutoInstallDuringOSUpgrade": true,
    "isAutoInstallOnApplicableSystems": true,
    "isDisclosureRestricted": false,
    "publishToWindows10s": false,
    "additionalInfoForMsApproval": {
      "microsoftContact": "abc@mcirosoft.com",
      "validationsPerformed": "Validation 1",
      "affectedOems": [
        "OEM1",
        "OEM2"
      ],
      "isRebootRequired": false,
      "isCoEngineered": true,
      "isForUnreleasedHardware": true,
      "hasUiSoftware": false,
      "businessJustification": "This is a business justification"
    }
  },
  "targeting": {
    "hardwareIds": [
      {
        "bundleId": "amd64",
        "infId": "foo.inf",
        "operatingSystemCode": "WINDOWS_v100_SERVER_X64_RS5_FULL",
        "pnpString": "hid\\vid_dummy256f&pid_dummyc62f",
        "distributionState": "pendingAdd"
      },
      {
        "bundleId": "amd64",
        "infId": "foo.inf",
        "operatingSystemCode": "WINDOWS_v100_RS2_FULL",
        "pnpString": "hid\\vid_dummy256f&pid_dummyc62f",
        "distributionState": "pendingAdd"
      }
    ],
    "chids": [
      {
        "chid": "346511cf-ccee-5c6d-8ee9-3c70fc7aae83",
        "distributionState": "pendingAdd"
      }
    ],
    "restrictedToAudiences": [
      "00000000-0000-0000-0000-000000000000",
      "00000000-0000-0000-0000-000000000001"
      ],
    "inServicePublishInfo": {
      "flooring": "RS1",
      "ceiling": "RS3"
    },
    "coEngDriverPublishInfo": {
      "flooringBuildNumber": 17135,
      "ceilingBuildNumber": 17139
    }
  },
  "workflowStatus": {
    "currentStep": "microsoftApproval",
    "state": "started",
    "messages": []
  },
  "links": [
    {
      "href": "https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606978459",
      "rel": "self",
      "method": "GET"
    },
    {
      "href": "https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606978459",
      "rel": "update_shippinglabel",
      "method": "PATCH"
    }
  ],
  "name": "VR_RS4Build_DualPublishCheck",
  "destination": "windowsUpdate"
}
```
### <a name="response-body"></a>响应正文

有关响应正文的详细信息，请参阅[发货标签资源](get-shipping-labels.md#shippinglabel-resource)。

## <a name="error-codes"></a>错误代码

有关错误代码的信息，请参阅[错误代码](get-product-data.md#error-codes)。

## <a name="see-also"></a>另请参阅

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
