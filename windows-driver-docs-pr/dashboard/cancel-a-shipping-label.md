---
title: 取消发货标签
description: 在 Microsoft 硬件 API 中使用此方法可请求取消处于“Microsoft 审批或逐步推出”状态的发货标签。
ms.topic: article
ms.date: 11/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7532f0275676300aa320449823c62dd70db21333
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "77072168"
---
# <a name="cancel-a-shipping-label"></a>取消发货标签

在 *Microsoft 硬件 API* 中使用此方法可请求取消处于“Microsoft 审批或逐步推出”状态的发货标签。 使用此方法之前，请确保你的发货标签处于“Microsoft 审批或逐步推出”状态。 有关获取发货标签的详细信息，请参阅[获取新的发货标签](get-a-shipping-label.md)。

## <a name="prerequisites"></a>必备条件

请先完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)（如果尚未这样做），然后再使用此方法。

## <a name="request"></a>请求

此方法具有以下语法。 本主题中的其他部分提供了标头和请求正文的用法示例和说明。

| 方法 | 请求 URI |
|:--|:--|
| PUT | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions/{submissionId}/shippingLabels/{shippingLabelId}/cancel` |

该方法中的 *productID*、*submissionID* 和 *shippingLabelId* 表示要取消的产品、提交和发货标签。

### <a name="request-header"></a>请求头

| Header | 类型 | 说明 |
|:--|:--|:--|
| Authorization | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** \<token\>。 |
| 接受 | 字符串 | 可选。 指定内容的类型。 允许的值是“application/json” |

### <a name="request-parameters"></a>请求参数

请勿为此方法提供请求参数。 

### <a name="request-body"></a>请求正文

请勿为此方法提供请求正文。 

### <a name="request-examples"></a>请求示例

以下示例演示如何请求取消发货标签。

```json
PUT https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964156/submissions/1152921504621467600/shippingLabels/1152921504606980300/cancel HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

响应将为空并且 HTTP 状态为 204。

完成此步骤后，请使用[获取发货标签](get-a-shipping-label.md)中的方法获取发货标签的更新详细信息。 请注意，在驱动程序外部测试系统中实际取消驱动程序可能需要一天以上的时间才能完成。

## <a name="error-codes"></a>错误代码

有关错误代码的更多信息，请参阅[错误代码](get-product-data.md#error-codes)。

## <a name="see-also"></a>另请参阅

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
