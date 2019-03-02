---
title: 与合作伙伴共享驱动程序
description: 若要将驱动程序与合作伙伴之一共享，请创建硬件提交并按照下面的步骤操作。
ms.assetid: BB69EF13-9271-4B17-BB42-A503BCDB0DE1
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffe84c58046ef7358cca109ab5da5e7bf47e6cc9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518152"
---
# <a name="share-a-driver-with-a-partner"></a>与合作伙伴共享驱动程序


若要将驱动程序与合作伙伴之一共享，请[创建硬件提交](create-a-new-hardware-submission.md)并按照下面的步骤操作。

**注意**  共享驱动程序只能由最初创建它的组织共享。 接收共享驱动程序的组织无法再次共享它。

 

1. [查找硬件提交](manage-your-hardware-submissions.md)，其中包含你想要共享的驱动程序。

2. 转到硬件提交的“分配”部分，然后选择“新发货标签”。

   ![显示“新建发货标签”按钮的屏幕截图](images/publish-new-shipping-label.png)

3. 在发货标签页面上，转到“详细信息”部分，然后在“发货标签名称”字段中输入发货标签的名称。 此名称是专用名称，不可供合作伙伴查看。 此名称允许你组织和搜索发货标签。

   ![显示标签名称和属性的屏幕截图](images/publish-label-name-share-new.png)

4. 在“属性”部分中，完成以下信息：

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

     

5. 在“目标”部分中，选择要共享的驱动程序包。

   ![显示发布目标设置的屏幕截图](images/publish-targeting-new.png)

6. 选择驱动程序包后，“选择 PNP”变为可用。 选择要共享的硬件 ID。 对于创建的任何发布，合作伙伴受限于所选的硬件 ID 值。 可使用硬件 ID 列表上方的搜索框搜索特定硬件 ID 或操作系统。

   -   若要面向所有列出的硬件 ID，请选择“全部发布”。

   -   若要面向特定硬件 ID，请查找每个所需的硬件 ID，然后选择“发布”。

   -   如果曾面向所有硬件 ID，但现在希望删除它们，请选择“全部过期”。

   -   若要删除对特定硬件 ID 的目标设定，请查找每个硬件 ID，然后选择“过期”。

7. 选择“发布”共享驱动程序。 如果不希望立即发布发货标签，可选择“保存”。 以后可通过打开发货标签并选择“发布”来发布发货标签，或者可从硬件提交页面中选择“发布所有待处理”。 请注意，选择“发布所有待处理”将发布所有未发布的发货标签。

 

 





