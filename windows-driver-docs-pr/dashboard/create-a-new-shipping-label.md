---
title: 创建新的发货标签
description: 此方法演示如何在 Microsoft 硬件 API 中创建新的发货标签。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: ab23c215ff9314138938d748f7d8792a714ec531
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63335032"
---
# <a name="create-a-new-shipping-label"></a>创建新的发货标签

在 *Microsoft 硬件API* 中使用此方法创建新的发货标签。 在使用此方法之前，请确保已经创建了一个产品并为该产品创建了提交。 有关详细信息，请参阅[创建产品](create-a-new-product.md)和[创建提交](create-a-new-submission-for-a-product.md)。

## <a name="prerequisites"></a>必备条件

完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)（如果尚未这样做），然后尝试使用这其中的任何方法。

## <a name="request"></a>请求

此方法具有以下语法。 请参阅以下部分，获取标头和请求正文的使用示例和描述。

| 方法 | 请求 URI |
|:--|:--|
| POST | `https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productID}/submissions/{submissionId}/shippingLabels` | 

方法中的 productID 和 submissionID 表示要为其创建发货标签的提交。

### <a name="request-header"></a>请求头

| 标头 | 在任务栏的搜索框中键入 | 描述 |
|:--|:--|:--|
| 授权 | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** \<token\>。 |
| 接受 | 字符串 | 可选。 指定内容的类型。 允许的值是“application/json” |


### <a name="request-parameters"></a>请求参数

请勿为此方法提供请求参数。 

### <a name="request-body"></a>请求正文

以下示例演示了用于创建新发货标签的 JSON 请求正文。

```json
{
  "publishingSpecifications": {
    "goLiveDate": "2018-02-22T06:50:54.793Z",
    "visibleToAccounts": [
      27691110,
      27691111
    ],
    "isAutoInstallDuringOSUpgrade": true,
    "isAutoInstallOnApplicableSystems": false,
    "isDisclosureRestricted": false,
    "publishToWindows10s": true,
    "additionalInfoForMsApproval": {
      "microsoftContact": "abc@microsoft.com",
      "validationsPerformed": "Validation 1",
      "affectedOems": [
        "OEM1",
        "OEM2"
      ],
      "isRebootRequired": false,
      "isCoEngineered": false,
      "isForUnreleasedHardware": false,
      "hasUiSoftware": false,
      "businessJustification": "This is a business justification"
    }
  },
  "targeting": {
    "hardwareIds": [
      {
        "bundleId": "3aba7558-10ca-42db-b1d1-57af5718aea3",
        "infId": "foo.inf",
        "operatingSystemCode": "WINDOWS_v100_RS3_FULL",
        "pnpString": "hid\\vid_dummy256f&pid_dummyc62f"
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
    }
  },
  "name": "Shipping Label Name",
  "destination": "windowsUpdate"
}
```

有关请求中的字段的详细信息，请参阅[发货标签资源](get-shipping-labels.md#shippinglabel-resource)。

#### <a name="points-to-remember-when-creating-shipping-labels"></a>创建发货标签时要记住的要点

- 发布到 Windows 更新时（*destination* 为 **windowsUpdate**），必须包括 [publishingSpecifications](get-shipping-labels.md#publishing-specifications-object) 对象。 对于自动安装（*isAutoInstallDuringOSUpgrade* 或 *isAutoInstallOnApplicableSystems* 为 true），必须设置 *additionalInfoForMsApproval*。
- 如果在发货标签中 *isAutoInstallDuringOSUpgrade* 或 *isAutoInstallOnApplicableSystems* 为真，则将发布驱动程序，并将“可以请求用户输入”设置为 false。
- 与其他合作伙伴共享时（*destination* 为 **anotherPartner**），必须包括 [recipientSpecifications](get-shipping-labels.md#recipient-specifications-object) 对象。

#### <a name="populating-targeting-information"></a>填充目标信息

**targeting** 对象包含指示 Windows 更新以下内容的数据：

- 如何根据硬件 ID 确定驱动程序的目标。

- 是否应该应用 CHID 或限制。

创建新的发货标签时，硬件 ID 对象应包含捆绑 ID、PNP ID、OS 代码和 INF 名称的有效组合。 下载驱动程序元数据文件（在获取提交的详细信息时以链接形式提供）以获取提交的这些属性允许的有效组合。 有关详细信息，请参阅[驱动程序包元数据](driver-package-metadata.md)。

### <a name="request-examples"></a>请求示例

以下示例演示了如何创建新产品。

```cpp
POST https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productID}/submissions/{submissionId}/shippingLabels HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

以下示例演示了创建发货标签的成功请求所返回的 JSON 响应正文。 有关响应正文中的值的详细信息显示在示例后面的表中。

```json
{
  "id": 1152921504606997500,
  "productId": 14461751976964156,
  "submissionId": 1152921504621467600,
  "publishingSpecifications": {
    "goLiveDate": "2018-02-22T06:50:54.793+00:00",
    "visibleToAccounts": [
      27691110,
      27691111
    ],
    "isAutoInstallDuringOSUpgrade": true,
    "isAutoInstallOnApplicableSystems": false,
    "isDisclosureRestricted": false,
    "publishToWindows10s": true,
    "additionalInfoForMsApproval": {
      "microsoftContact": "abc@microsoft.com",
      "validationsPerformed": "Validation 1",
      "affectedOems": [
        "OEM1",
        "OEM2"
      ],
      "isRebootRequired": false,
      "isCoEngineered": false,
      "isForUnreleasedHardware": false,
      "hasUiSoftware": false,
      "businessJustification": "This is a business justification"
    }
  },
  "workflowStatus": {
    "currentStep": "preProcessShippingLabel",
    "state": "notStarted",
    "messages": []
  },
  "links": [
    {
      "href": "https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606997603",
      "rel": "self",
      "method": "GET"
    },
    {
      "href": "https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606997603",
      "rel": "update_shippinglabel",
      "method": "PATCH"
    }
  ],
  "name": "Shipping Label Name",
  "destination": "windowsUpdate"
}
```

### <a name="response-body"></a>响应正文

有关响应正文的详细信息，请参阅[发货标签资源](get-shipping-labels.md#shippinglabel-resource)。

## <a name="error-codes"></a>错误代码

有关错误代码的信息，请参阅[错误代码](get-product-data.md#error-codes)。

## <a name="see-also"></a>另请参阅

[硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
