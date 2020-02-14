---
title: 管理发货标签
description: 本文档包含有关如何在硬件仪表板中创建或更新驱动程序提交的发货标签的信息
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 08/23/2018
ms.openlocfilehash: 37b268df879ad4d591fcaab034699fd45096d86d
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072156"
---
# <a name="manage-shipping-labels"></a>管理发货标签

使用以下方法管理 Windows 硬件仪表板提交的发货标签。 有关 Microsoft 硬件仪表板 API 的简介，包括使用该 API 的先决条件，请参阅[硬件仪表板 API](dashboard-api.md)。

```cpp
https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productid}/submissions/{submissionid}/shippingLabels
```

管理发货标签的方法

|说明|方法 |URI|
|:--|:--|:--|
|[创建新的发货标签](create-a-new-shipping-label.md)|POST|`https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productid}/submissions/{submissionid}/shippingLabels`|
|[更新发货标签](update-a-shipping-label.md)|修补程序|`https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productid}/submissions/{submissionid}/shippingLabels/{shippingLabelId}`|
|[取消发货标签](cancel-a-shipping-label.md)|PUT|`https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productid}/submissions/{submissionid}/shippingLabels/{shippingLabelId/cancel}`|

## <a name="create-a-new-shipping-label"></a>创建新的发货标签

1. 如果尚未开始操作，请先完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)。

2. [获取 Azure AD 访问令牌](dashboard-api.md#obtain-an-azure-ad-access-token)。 在 Microsoft Store 提交 API 中，必须将此访问令牌传递给相关方法。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。

3. 应该已创建了产品和提交，以便创建发货标签。 有关创建产品和提交的详细信息，请参阅[管理产品提交](manage-product-submissions.md)。

4. 通过执行以下方法为此提交[创建新的发货标签](create-a-new-shipping-label.md)。  使用在上一步中在[管理产品提交](manage-product-submissions.md)中创建的 ProductID 和 SubmissionID。

    ```cpp
    https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productid}/submissions/{submissionid}/shippingLabels
    ```
    响应正文包含[发货标签资源](get-shipping-labels.md#shippinglabel-resource)，其中包含新创建的发货标签的 ID 和其他详细信息。

## <a name="code-examples"></a>代码示例

以下代码示例演示了如何使用 Microsoft 硬件 API：

* [C# 示例](https://download.microsoft.com/download/C/F/4/CF404E53-87A0-4204-BA13-A64B09A237C1/HardwareApiCSharpSample.zip)

## <a name="data-resources"></a>数据资源

用于创建和管理产品数据的 Microsoft 硬件 API 方法使用以下 JSON 数据资源：

* [发货标签资源](get-shipping-labels.md#shippinglabel-resource)

## <a name="error-codes"></a>错误代码

有关错误代码的信息，请参阅[错误代码](get-product-data.md#error-codes)。

## <a name="see-also"></a>另请参阅

- [硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
