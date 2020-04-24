---
title: 与合作伙伴共享驱动程序
description: 若要将驱动程序与合作伙伴之一共享，请创建硬件提交并按照下面的步骤操作。
ms.assetid: BB69EF13-9271-4B17-BB42-A503BCDB0DE1
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b4fe3e6b949d5bc327b8638b9bcf65852a93a7d
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "79243060"
---
# <a name="share-a-driver-with-a-partner"></a>与合作伙伴共享驱动程序


若要将驱动程序与合作伙伴之一共享，请[创建硬件提交](create-a-new-hardware-submission.md)并按照下面的步骤操作。

**注意**  共享驱动程序只能由最初创建它的组织共享。 接收共享驱动程序的组织无法再次共享它。

 

1. [查找硬件提交](manage-your-hardware-submissions.md)，其中包含你想要共享的驱动程序。

2. 转到硬件提交的“分配”  部分，然后选择“新发货标签”  。

   ![显示“新建发货标签”按钮的屏幕截图](images/publish-new-shipping-label.png)

3. 在发货标签页面上，转到“详细信息”  部分，然后在“发货标签名称”  字段中输入发货标签的名称。 此名称是私人名称，不会向合作伙伴显示。 此名称允许你组织和搜索发货标签。

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
   <th>说明</th>
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

6. 选择驱动程序包后，会显示“选择 PNP”网格  。 可使用硬件 ID 列表上方的搜索框搜索特定硬件 ID 或操作系统。  对于合作伙伴创建的任何发布内容，合作伙伴只能使用你共享的硬件 ID 值。 

   -   若要针对所有列出的硬件 ID，请选择“全部共享”  。

   -   若要针对特定硬件 ID，请查找每个所需的硬件 ID，然后选择“共享”  。

   -   如果以前针对了所有硬件 ID，但现在希望删除它们，请选择“全部撤消”  。

   -   若要删除对特定硬件 ID 的目标设定，请查找每个硬件 ID，然后选择“撤消”  。

7. 选择底部的“发布”以完成驱动程序共享  。 如果不希望立即发布发货标签，可选择“保存”  。 以后可通过打开发货标签并选择“发布”  来发布发货标签，或者可从硬件提交页面中选择“发布所有待处理”  。 请注意，选择“发布所有待处理”  将发布所有未发布的发货标签。

## <a name="span-idrevokespanrevokerevoke-all"></a><span id="Revoke"></span>撤消/全部撤消：  

从共享的发货标签中撤消硬件 ID 会发生以下情况。

1.  接收方一端的现有提交 ID 将被弃用。

2.  新的专用产品 ID 和提交 ID 以及调整的硬件 ID 将与合作伙伴共享。  此新实体具有相同的共享产品 ID。  如果选择了“全部撤消”，则会删除所有硬件 ID  。

3.  当合作伙伴尝试为 Windows 更新创建**新的**发货标签时，其可用硬件 ID 列表将反映所做的更改，仅列出共享的硬件 ID。  如果选择了“全部撤消”，其硬件 ID 网格将是空的  。

> [!NOTE]
> 如果合作伙伴已将其共享的发货标签发布到 Windows 更新，则撤消硬件 ID **不会**从 Windows 更新目录中删除其现有项。  该项会保持发布状态，直到该合作伙伴使其过期。
>
> 使用合作伙伴创建的现有发货标签只能使已弃用发货标签上的内容过期。
>
> 已弃用发货标签中已签名的驱动程序和 DUA Shell 包仍可供合作伙伴下载。
>
> 共享和撤消硬件 ID 不会修改原始 INF。
