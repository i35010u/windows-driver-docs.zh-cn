---
title: 更新产品数据
description: Microsoft 硬件 API 中的此方法可更新产品的详细信息。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2c1398e0480362f3be2ec85e9231e1a5d24a331c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518090"
---
# <a name="update-product-data"></a>更新产品数据  
使用 Microsoft 硬件 API 中的此方法可更新产品的详细信息。 使用此方法之前，请确保已创建了产品。 有关详细信息，请参阅[创建新产品](create-a-new-product.md)。 

## <a name="prerequisites"></a>必备条件 
如果尚未开始操作，请先完成 Microsoft 硬件 API 的所有先决条件，然后再尝试使用其中任何方法。 
 
## <a name="request"></a>请求 
此方法具有以下语法。 请参阅以下部分，获取标头和请求正文的使用示例和描述。 


| 方法 | 请求 URI |
|:--|:--|
| 修补程序 | `https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productID}` |

### <a name="request-header"></a>请求头

| 标头 | 在任务栏的搜索框中键入 | 描述 |
|:--|:--|:--|
| 授权 | 字符串    | 必需。 Azure AD 访问令牌的格式为 **Bearer** \<token\>。 |
| accept |  字符串 | 可选。 指定内容的类型。 允许的值是“application/json” |

### <a name="request-parameters"></a>请求参数

请勿为此方法提供请求参数。

### <a name="request-body"></a>请求正文

以下示例演示了用于更新产品的 JSON 请求正文。 只能对产品进行三种类型的更改 - announcementDate、marketingNames 和 productName。

```json 
{
  "announcementDate": "2018-04-05T08:59:03.414Z",
  "marketingNames": ["name1"],
  "productName": "updatedProductName"
}
```

有关请求中的字段的详细信息，请参阅[产品资源](get-product-data.md#product-resource)。

### <a name="request-examples"></a>请求示例
以下示例演示了如何更新产品。

```json 
PATCH https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/14631253285588838 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

响应将为空并且 HTTP 状态为 204。

完成此步骤后，请使用[获取产品详细信息](get-a-product.md)方法来获取更新的产品详细信息。

## <a name="error-codes"></a>错误代码
有关详细信息，请参阅[错误代码](get-product-data.md#error-codes)。

## <a name="see-also"></a>另请参阅

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
