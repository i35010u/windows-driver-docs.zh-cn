---
title: 获取提交的所有发货标签的数据
description: Microsoft 硬件 API 中的这些方法可获取注册到硬件仪表板帐户的硬件产品的发货标签。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: 59fbf44a5cf8f5a1cdf7cb588bab751cfecab114
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518507"
---
# <a name="get-all-shipping-labels"></a>获取所有发货标签

使用 Microsoft 硬件 API 中的此方法可检索产品的特定提交的所有发货标签数据。

## <a name="prerequisites"></a>必备条件

完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)（如果尚未这样做），然后尝试使用这其中的任何方法。 在使用这些方法之前，产品和提交必须已存在于你的开发人员中心帐户中。 若要创建或管理产品提交，请参阅[管理产品提交](manage-product-submissions.md)中的方法。

## <a name="request"></a>请求

此方法具有以下语法。 请参阅以下部分，获取标头和请求正文的使用示例和描述。

|方法|请求 URI|
|--|--|
|GET|`https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productId}/submissions/{submissionId}/shippingLabels/`|

### <a name="request-header"></a>请求头

|标头|在任务栏的搜索框中键入|描述|
|--|--|--|
|授权|字符串|必需。 Azure AD 访问令牌的格式为 **Bearer** \*<token\>*。|
|accept|字符串|可选。 指定内容的类型。 允许的值是“application/json”|

### <a name="request-parameters"></a>请求参数

请勿为此方法提供请求参数。

### <a name="request-body"></a>请求正文

请勿为此方法提供请求正文。

### <a name="request-examples"></a>请求示例

以下示例演示了如何检索注册到帐户的所有产品的相关信息。

```cpp
GET https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/ HTTP/1.1
Authorization: Bearer <your access token>
```
## <a name="response"></a>响应

下面的示例演示了一个成功请求返回的 JSON 响应正文，该请求针对注册到开发者帐户的特定产品提交的所有发货标签。 为简洁起见，此示例仅显示该请求返回的前三个发货标签。 有关响应正文中的值的详细信息显示在示例后面的表中。

```json
{
  "value": [
    {
      "id": 1152921504606980300,
      "productId": 14461751976964156,
      "submissionId": 1152921504621467600,
      "publishingSpecifications": {
        "goLiveDate": "2018-04-04T16:11:27.2965057+00:00",
        "visibleToAccounts": [],
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
      "workflowStatus": {
        "currentStep": "microsoftApproval",
        "state": "started",
        "messages": []
      },
      "links": [
        {
          "href": "https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606980231",
          "rel": "self",
          "method": "GET"
        },
        {
          "href": "https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606980231",
          "rel": "update_shippinglabel",
          "method": "PATCH"
        }
      ],
      "name": "Publish to Windows Update with promotions",
      "destination": "windowsUpdate"
    },
    {
      "id": 1152921504606978500,
      "productId": 14461751976964156,
      "submissionId": 1152921504621467600,
      "recipientSpecifications": {
        "receiverPublisherId": "27691110",
        "enforceChidTargeting": false
      },
      "workflowStatus": {
        "currentStep": "finalizeSharing",
        "state": "completed",
        "messages": []
      },
      "links": [
        {
          "href": "https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606978460",
          "rel": "self",
          "method": "GET"
        },
        {
          "href": "https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606978460",
          "rel": "update_shippinglabel",
          "method": "PATCH"
        }
      ],
      "name": "Share submission with another Partner",
      "destination": "anotherPartner"
    },
    {
      "id": 1152921504606978500,
      "productId": 14461751976964156,
      "submissionId": 1152921504621467600,
      "publishingSpecifications": {
        "goLiveDate": "2018-04-03T04:50:52.2293001+00:00",
        "visibleToAccounts": [],
        "isAutoInstallDuringOSUpgrade": false,
        "isAutoInstallOnApplicableSystems": false,
        "isDisclosureRestricted": false,
        "publishToWindows10s": false
      },
      "workflowStatus": {
        "currentStep": "finalizePublishing",
        "state": "completed",
        "messages": []
      },
      "links": [
        {
          "href": "https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606978538",
          "rel": "self",
          "method": "GET"
        },
        {
          "href": "https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606978538",
          "rel": "update_shippinglabel",
          "method": "PATCH"
        }
      ],
      "name": "Publish to Windows Update without promotions",
      "destination": "windowsUpdate"
    }
  ],
  "links": [
    {
      "href": "https://manage.devcenter.microsoft.com/v1.0/my/hardware/products?pageSize=50",
      "rel": "self",
      "method": "GET"
    }
  ]
}
```
此资源具有以下值

| 值 | 在任务栏的搜索框中键入 | 描述 |
|:--|:--|:--|
| value | 数组 | 一个对象数组，其中包含有关每个发货标签的信息。 有关每个对象中的数据的详细信息，请参阅[发货标签资源](get-shipping-labels.md#shippinglabel-resource)。 |
| links | 数组 | 一个对象数组，其中包含有关包含实体的有用链接。 有关更多详细信息，请参阅[链接对象](get-product-data.md#link-object)。|

## <a name="error-codes"></a>错误代码

有关错误代码的信息，请参阅[错误代码](get-product-data.md#error-codes)。

## <a name="see-also"></a>另请参阅

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
