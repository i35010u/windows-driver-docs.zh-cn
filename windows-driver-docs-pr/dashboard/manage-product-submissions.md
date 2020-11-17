---
title: 管理产品提交
description: 管理产品的硬件仪表板提交，并让 Microsoft 对产品签名
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: c5d8dae75eb63d186f8f0c18b108d5e2c575ec8c
ms.sourcegitcommit: 34bc742a0de40bcc4eda99f32622c58584a7f9f2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384175"
---
# <a name="manage-product-submissions"></a>管理产品提交

使用 *Microsoft 硬件 API* 中的以下方法管理产品提交并让 Microsoft 对产品签名。 有关 Microsoft 硬件 API 的简介，包括使用该 API 的先决条件，请参阅[硬件仪表板 API](dashboard-api.md)。

```cpp
https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/
```

管理产品提交的方法

| 方法 | URI | 说明 |
|:--|:--|:--|
| GET | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}` | [获取某个特定产品的状态/数据](get-a-product.md)  |
| GET | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions/{submissionId}` |[获取产品的特定提交的状态/数据](get-a-submission.md)   |
| POST | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products` | [创建新产品](create-a-new-product.md)   |
| POST | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions/` | [为产品创建新的提交](create-a-new-submission-for-a-product.md)  |
| POST | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions/{submissionId}/commit` |[确认产品提交](commit-a-product-submission.md)  |

## <a name="create-and-submit-a-product-for-signing"></a>创建并提交产品以进行签名

1. 如果尚未开始操作，请先完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)。

2. [获取 Azure AD 访问令牌](dashboard-api.md#obtain-an-azure-ad-access-token)。 在 Microsoft Store 提交 API 中，必须将此访问令牌传递给相关方法。 获取访问令牌后，在它到期前，你有 60 分钟的使用时间。 该令牌到期后，可以获取新的令牌。

3. 通过执行 Microsoft 硬件 API 中的以下方法[创建新产品](create-a-new-product.md)。 这会创建一个新的在建产品，并允许你提交该产品的程序包。

    ```cpp
    https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/
    ```

    响应正文包含[产品资源](get-product-data.md#product-resource)，此资源包括此产品的 ID。

4. 通过执行 Microsoft 硬件 API 中的以下方法为此产品[创建新提交](create-a-new-submission-for-a-product.md)。  使用上述步骤中创建的 ProductID。

    ```cpp
    https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions/
    ```

    响应正文包含[提交资源](get-product-data.md#submission-resource)，此资源包括提交 ID、用于上传产品（驱动程序）包以提交到 Azure Blob 存储的共享访问签名 (SAS) URI。 [!NOTE] > SAS URI 提供对 Azure 存储中的安全资源的访问权限（无需帐户密钥）。 有关 SAS URI 及其与 Azure Blob 存储一起使用的背景信息，请参阅[共享访问签名（第 1 部分）：了解 SAS 模型](/azure/storage/common/storage-sas-overview)和[共享访问签名（第 2 部分）：创建 SAS 并将其与 Blob 存储一起使用](/azure/storage/common/storage-sas-overview)。

5. **上传你的程序包** 到 Azure Blob 存储中的某个位置，此位置由上一个步骤中的 SAS URI 指定。
以下 C# 代码示例演示如何在用于 .NET 的 Azure 存储客户端库中使用 [CloudBlockBlob](/dotnet/api/microsoft.azure.storage.blob.cloudblockblob/) 类将程序包上传到 Azure Blob 存储。 此示例假定程序包已写入流对象。

    ```json
    string sasUrl = "https://productingestionbin1.blob.core.windows.net/ingestion/26920f66-b592-4439-9a9d-fb0f014902ec?sv=2014-02-14&sr=b&sig=usAN0kNFNnYE2tGQBI%2BARQWejX1Guiz7hdFtRhyK%2Bog%3D&se=2016-06-17T20:45:51Z&sp=rwl";
    Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob blockBob =
        new Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob(new System.Uri(sasUrl));
    await blockBob.UploadFromStreamAsync(stream);
    ```

6. 通过执行以下方法[确认产品提交](commit-a-product-submission.md)。 这将通知硬件开发人员中心你已完成产品提交并且将开始对提交进行验证。

    ```cpp
    https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions/{submissionId}/commit
    ```

7. 通过执行以下方法来检查提交状态以[获取产品提交的状态](get-a-submission.md)。

    ```cpp
    https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions/{submissionId}
    ```

    若要确认提交状态，请查看响应正文中的 **commitStatus** 值。 如果请求成功，此值应该从 CommitReceived 更改为 CommitComplete；如果请求中存在错误，此值应该更改为 CommitFailed  。 如果存在错误，error  字段将包含有关错误的更多详细信息。

   >[!NOTE]
   >“搜索”主页大约每隔 10 分钟刷新一次。 若要在创建时查看所有结果，请单击合作伙伴中心的“驱动程序”页顶部的“驱动程序列表页(全部)”。   如果提交了大量的请求，页面处理和加载需要花费一段时间，不过，在加载后，应会列出成功和失败的提交。 有关详细信息，请参阅[查找硬件提交](./find-hardware-submission.md)。

## <a name="code-examples"></a>代码示例

以下代码示例演示了如何使用 Microsoft 硬件 API：

* [C# 示例](https://download.microsoft.com/download/C/F/4/CF404E53-87A0-4204-BA13-A64B09A237C1/HardwareApiCSharpSample.zip)

## <a name="data-resources"></a>数据资源

用于创建和管理产品数据的 Microsoft 硬件 API 方法使用以下 JSON 数据资源：

* [产品资源](get-product-data.md#product-resource)

* [提交资源](get-product-data.md#submission-resource)

## <a name="see-also"></a>另请参阅

[硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
