---
title: 创建发布者驱动程序元数据
description: 介绍用于为合作伙伴中心提交创建发布者驱动程序包元数据的 API 调用。
author: VanathiGanesh
ms.author: vaganesh
ms.topic: article
ms.date: 11/06/2019
ms.openlocfilehash: 8c87896d245c2eb4ba3502f438d1448e696d464e
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "77072220"
---
# <a name="create-publisher-driver-metadata"></a>创建发布者驱动程序元数据

在 Microsoft 硬件 API 中使用此方法可为与你共享的提交创建发布者驱动程序元数据。 不能为收件箱或系统提交创建发布者驱动程序元数据。 若要了解有关驱动程序元数据包的详细信息，请参阅[驱动程序包元数据](driver-package-metadata.md)页面。

## <a name="prerequisites"></a>必备条件

完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)（如果尚未这样做），然后尝试使用这其中的任何方法。

## <a name="request"></a>请求

此方法具有以下语法。 请参阅以下部分，获取标头和请求正文的使用示例和描述。


| 方法 | 请求 URI                                                                                                    |
|:-------|:---------------------------------------------------------------------------------------------------------------|
| POST   | https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions/{submissionID}/createpublishermetadata |

### <a name="request-header"></a>请求头

| Header | 类型 | 说明 |
|:--|:--|:--|
| Authorization | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** \<token\>。 |
| accept | 字符串 | 可选。 指定内容的类型。 允许的值是“application/json” |

### <a name="request-parameters"></a>请求参数

请勿为此方法提供请求参数。

### <a name="request-body"></a>请求正文

请勿为此方法提供请求正文。

### <a name="request-examples"></a>请求示例

以下示例演示了如何为提交创建发布者驱动程序元数据。

```cpp
POST https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14631253285588838/submissions/1152921504621465124/createpublishermetadata HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

### <a name="response-body"></a>响应正文

响应将为空并且 HTTP 状态为 202。

完成此步骤后请等待几个小时，发布者驱动程序元数据需要几个小时才能完成创建。 然后，使用方法[获取提交详细信息](get-a-submission.md)来获取发布者驱动程序元数据文件的链接。

## <a name="error-codes"></a>错误代码

有关详细信息，请参阅[错误代码](get-product-data.md#error-codes)。

## <a name="see-also"></a>另请参阅

[硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
