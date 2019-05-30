---
title: 与合作伙伴共享驱动程序
description: 若要将驱动程序与合作伙伴之一共享，请创建硬件提交并按照下面的步骤操作。
ms.assetid: BB69EF13-9271-4B17-BB42-A503BCDB0DE1
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b4fe3e6b949d5bc327b8638b9bcf65852a93a7d
ms.sourcegitcommit: a0da18a4c5c636c4980e8ed77c6879e617299580
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66373153"
---
# <a name="share-a-driver-with-a-partner"></a>与合作伙伴共享驱动程序


若要将驱动程序与合作伙伴之一共享，请[创建硬件提交](create-a-new-hardware-submission.md)并按照下面的步骤操作。

**注意**  共享驱动程序只能由最初创建它的组织共享。 接收共享驱动程序的组织无法再次共享它。

 

1. [查找硬件提交](manage-your-hardware-submissions.md)，其中包含你想要共享的驱动程序。

2. 转到硬件提交的“分配”  部分，然后选择“新发货标签”  。

   ![显示“新建发货标签”按钮的屏幕截图](images/publish-new-shipping-label.png)

3. 在发货标签页面上，转到“详细信息”  部分，然后在“发货标签名称”  字段中输入发货标签的名称。 此名称是私有的并且不会显示由您的合作伙伴。 此名称允许你组织和搜索发货标签。

   ![显示标签名称和属性的屏幕截图](images/publish-label-name-share-new.png)

4. 在“属性”  部分中，完成以下信息：

   <table>
   <colgroup>
   <col width="50%" />
   <col width="50%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th>字段</th>
   <th>描述</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td><p><strong>目标</strong></p></td>
   <td><p>选择“发送到另一个合作伙伴”与合作伙伴共享驱动程序。 如果要为 Windows 更新创建发货标签，请参阅<a href="publish-a-driver-to-windows-update.md" data-raw-source="[Publish a driver to Windows Update](publish-a-driver-to-windows-update.md)">将驱动程序发布到 Windows 更新</a>。</p></td>
   </tr>
   <tr class="even">
   <td><p><strong>发布者是谁？</strong></p></td>
   <td><p>搜索合作伙伴的公司名称，然后选择它。</p></td>
   </tr>
   <tr class="odd">
   <td><p><strong>要求按接收方设定 CHID 目标</strong></p></td>
   <td><p>此选项强制合作伙伴将 CHID 应用到他们基于你的驱动程序创建的所有发布请求。 这使你可以在多个合作公司之间共享硬件 ID 时保护用户。</p></td>
   </tr>
   </tbody>
   </table>
   
5. 在“目标”  部分中，选择要共享的驱动程序包。

   ![显示发布目标设置的屏幕截图](images/publish-targeting-new.png)

6. 选择驱动程序包之后,**选择 PNPs**网格变得可用。 可以使用硬件 Id 列表上方的搜索框搜索特定的硬件 ID 或操作系统。  你的合作伙伴被限制为它们创建任何发布共享的硬件 ID 值。 

   -   若要针对所有列出的硬件 Id，请选择**共享所有**。

   -   若要针对特定硬件 Id，查找每个所需的硬件 ID，并选择**共享**。

   -   如果你针对的所有硬件 Id 并且想要将其删除，则选择**Revoke All**。

   -   若要删除目标为特定的硬件 Id，查找每个硬件 ID，并选择**撤消**。

7. 选择**发布**最底部以完成驱动程序的共享。 如果不希望立即发布发货标签，可选择“保存”  。 以后可通过打开发货标签并选择“发布”  来发布发货标签，或者可从硬件提交页面中选择“发布所有待处理”  。 请注意，选择“发布所有待处理”  将发布所有未发布的发货标签。

## <a name="span-idrevokespanrevokerevoke-all"></a><span id="Revoke"></span>撤消/撤销所有：  

撤消共享的发货标签从一个硬件 ID 将执行以下操作。

1.  在接收方端现有的提交 ID 将被弃用。

2.  将与你的合作伙伴共享的新专用产品 ID 和提交 ID 为调整后的硬件 Id。  此新的实体将具有相同的共享产品 id。  如果所选**Revoke All**则会删除所有硬件 Id。

3.  当尝试创建你的合作伙伴**新建**Windows 更新发运标签，其可用的硬件 Id 的列表将反映所做的更改，并仅列出共享了这些硬件 Id。  在中**Revoke All**的情况下，其硬件 ID 网格将为空。

> [!NOTE]
> 如果你的合作伙伴已经发布到 Windows 更新其共享的邮寄标签，撤消硬件 ID**不会删除**Windows 更新目录从其现有项。  它将保持该合作伙伴过期它之前已发布。
>
> 仅允许由你的合作伙伴创建的现有发货标签过期不推荐使用的发货标签上的内容。
>
> 仍可由合作伙伴下载签名的驱动程序和中不推荐使用的发货标签的 DUA Shell 包。
>
> 共享和撤消硬件 ID 不会修改原始 INF。
