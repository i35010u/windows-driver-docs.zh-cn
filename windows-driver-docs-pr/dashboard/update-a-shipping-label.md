---
title: 更新发货标签
description: 此方法更新硬件仪表板 API 中的发货标签。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: 65cd448a3ed862f61cbe7fb894c19b3e87d40b96
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "77072154"
---
# <a name="update-a-shipping-label"></a>更新发货标签

在 *Microsoft 硬件API* 中使用此方法更新发货标签。 使用此方法之前，请确保已创建发货标签。 有关创建发货标签的详细信息，请参阅[创建新的发货标签](create-a-new-shipping-label.md)。

## <a name="prerequisites"></a>必备条件

完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)（如果尚未这样做），然后再使用这其中的任何方法。

## <a name="request"></a>请求

此方法具有以下语法。 本主题中的其他部分提供了标头和请求正文的用法示例和说明。

| 方法 | 请求 URI |
|:--|:--|
| 修补程序 | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions/{submissionId}/shippingLabels/{shippingLabelId}` |

方法中的 productID  、submissionID  和 shippingLabelId  表示要更新的产品、提交和发货标签。

### <a name="request-header"></a>请求头

| Header | 类型 | 说明 |
|:--|:--|:--|
| Authorization | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** \<token\>。 |
| 接受 | 字符串 | 可选。 指定内容的类型。 允许的值是“application/json” |

### <a name="request-parameters"></a>请求参数

请勿为此方法提供请求参数。 

### <a name="request-body"></a>请求正文

以下示例演示了发货标签的 JSON 请求正文。 只能对发货标签进行以下类型的更改：

* 添加硬件 ID
* 删除硬件 ID/使硬件 ID 过期
* 添加 CHID
* 删除 CHID
* 添加受众
* 更新/删除受众
* 为更改提供业务理由

```json
{
  "targetingInfo": {
    "chids": [
      {
        "chid": "812fac65-9c26-473c-b3a9-1eb3803ac22c",
        "action": "add"
      },
      {
        "chid": "aed6336d-0958-444c-89b6-bf471191d6f0",
        "action": "remove"
      }
    ],
    "hardwareIds": [
      {
        "action": "remove",
        "bundleId": "a2dfbcd8-1d4a-4885-90a3-2ac8360542da",
        "infId": "foo.inf",
        "operatingSystemCode": "WINDOWS_v100_X64_RS3_FULL",
        "pnpString": "pci\\ven_8086&dev_5a85"
      },
      {
        "action": "add",
        "bundleId": "48140805-45a3-4a76-8818-e75c117adba9",
        "infId": "foo.inf",
        "operatingSystemCode": "WINDOWS_v100_X64_RS3_FULL",
        "pnpString": "pci\\ven_8086&dev_5a85"
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
    "businessJustification": "Business justification for updating shipping label"
  }
}
```

有关请求中的字段的详细信息，请参阅[发货标签资源](get-shipping-labels.md#shippinglabel-resource)。

需要注意的要点：

* 更新 CHID 或 HardwareID 时，必须为“操作”  提供值。

* “受众”  是仅更新字段。 在此字段中提供值将覆盖以前的任何值。 将此值留空将删除上一个值。

* 若要了解如何获取组织的受众列表，请参阅[获取受众](get-audience-data.md)。

* 创建新的发货标签时，硬件 ID 对象应包含捆绑 ID、PNP ID、OS 代码和 INF 名称的有效组合。 若要获取提交（包）的这些属性的有效、允许组合，请在获取提交的详细信息时下载驱动程序元数据文件（以链接形式提供）。 有关详细信息，请参阅[驱动程序包元数据](driver-package-metadata.md)。

### <a name="request-examples"></a>请求示例

以下示例演示了如何更新产品。

```json
PATCH https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964156/submissions/1152921504621467600/shippingLabels/1152921504606980300 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

响应将为空并且 HTTP 状态为 204。

完成此步骤后，请使用[获取发货标签](get-a-shipping-label.md)中的方法获取发货标签的更新详细信息。

## <a name="error-codes"></a>错误代码

有关错误代码的更多信息，请参阅[错误代码](get-product-data.md#error-codes)。

## <a name="see-also"></a>另请参阅

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
