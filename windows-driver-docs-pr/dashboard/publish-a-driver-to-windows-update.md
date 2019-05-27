---
title: 将驱动程序发布到 Windows 更新
description: 若要将驱动程序发布到 Windows 更新，请创建硬件提交，然后按照下面的步骤操作。
ms.assetid: E62AADCF-E481-40CA-98F1-BE4629C3EE35
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f991824cba8ebda7fdd053c89776b6f2cd2458db
ms.sourcegitcommit: 998c5840ce92a50ae42127101e4ecc19a5e362c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "65996961"
---
# <a name="publish-a-driver-to-windows-update"></a>将驱动程序发布到 Windows 更新


若要将驱动程序发布到 Windows 更新，请[创建硬件提交](create-a-new-hardware-submission.md)，然后按照下面的步骤操作。

1. [查找硬件提交](manage-your-hardware-submissions.md)，该提交中包含你想要分发的驱动程序。

2. 转到硬件提交的“分配”部分，然后选择“新发货标签”。

   ![显示“新建发货标签”按钮的屏幕截图](images/publish-new-shipping-label.png)

3. 在发货标签页面上，转到“详细信息”部分，然后在“发货标签名称”字段中输入发货标签的名称。 此名称允许你组织和搜索发货标签。

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
   <td><p>选择“发布到 Windows 更新”将驱动程序发布到 Windows 更新。 如果要创建允许你与合作伙伴共享驱动程序的共享发货标签，请参阅<a href="sharing-drivers-with-your-partners.md" data-raw-source="[Share a driver with a partner](sharing-drivers-with-your-partners.md)">与合作伙伴共享驱动程序</a>。</p>
   <div class="alert">
   <strong>注意</strong>  共享驱动程序只能由最初创建它的组织共享。 接收共享驱动程序的组织无法再次共享它。
   </div>
   <div>
     
   </div></td>
   </tr>
   <tr class="even">
   <td><p><strong>指定合作伙伴（如果有），使其获得对此请求的可见性</strong></p></td>
   <td><p>输入希望其具有驱动程序和发货标签的只读权限的合作伙伴。 希望合作伙伴注意此发货标签请求时（例如当代表他们发布驱动程序时），使用此字段。 有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/mt786462" data-raw-source="[Publish a driver on behalf of a partner](https://msdn.microsoft.com/library/windows/hardware/mt786462)">代表合作伙伴发布驱动程序</a>。</p></td>
   </tr>
   <tr class="odd">
   <td><p><strong>驱动程序推广</strong></p></td>
   <td><p>默认情况下，Windows 更新上的驱动程序标记为可选。 这意味着，仅在设备尚未安装驱动程序时才交付驱动程序。 这些选项允许你替代默认行为，但需要额外 Microsoft 评估。</p>
   <p>选择“在 Windows 升级期间自动交付和安装此驱动程序”推广驱动程序，使其可用于动态更新。</p>
   <p>选择“在所有适用的系统上自动交付和安装此驱动程序”将驱动程序推广到“关键”。</p></td>
   </tr>
   </tbody>
   </table>

   ![显示标签名称和发布属性的屏幕截图](images/label-name-and-properties-windows-update.png)

5. 在“目标”部分中，选择要发布的驱动程序包。

6. 选择驱动程序包后，“选择 PNP”变为可用。 选择要面向的硬件 ID。 可使用硬件 ID 列表上方的搜索框搜索特定硬件 ID 或操作系统。

   若要面向所有列出的硬件 ID，请选择“全部发布”。

   若要面向特定硬件 ID，请查找每个所需的硬件 ID，然后选择“发布”。

   如果曾面向所有硬件 ID，但现在希望删除它们，请选择“全部过期”。

   若要删除对特定硬件 ID 的目标设定，请查找每个硬件 ID，然后选择“过期”。

   ![显示目标部分和 PNP 的屏幕截图](images/publish-targeting-windows-update.png)

7. 如果要添加计算机硬件 ID (CHID)，请在文本框中输入每个 CHID，然后选择“添加 CHID”。 若要批量添加多个 CHID，请确保每个 CHID 都由换行符分隔、选择“添加多个 CHID”，然后将 CHID 粘贴到文本框。 可在文本框下方的列表中查看所有添加的 CHID。 若要从列表中删除 CHID，请选择“删除”

>[!IMPORTANT]
> 以下 Windows 版本不支持 CHID：
> * Windows 8.1 或更低版本
> * Windows Server 2012 R2 或更低版本
>
> 如果你的驱动程序面向这些操作系统中的任何一个，请创建两个发货标签：一个用于 Windows 10（可以在其中添加 CHID），另一个用于低级别操作系统（不会在其中添加 CHID）。



8. 如果你希望限制在 Windows 更新目录和 WSUS 目录中公开披露你的发货标签，请选中“限制此发货标签信息的公开披露”。 box.  

   ![显示限制公开披露的屏幕截图](images/limit-public-disclosure.PNG)

   你的驱动程序仍然可以从 Windows 更新发布和下载，但不会显示在任何公共目录列表中。

9. 如果驱动程序面向处于 S 模式的 Windows 10，则必须将两个框都选中，并确认满足以下条件：

   * 驱动程序兼容且遵循[处于 S 模式的 Windows 10 驱动程序要求](https://docs.microsoft.com/windows-hardware/drivers/install/Windows10SDriverRequirements)中所述的驱动程序策略。
   * 确保驱动程序遵循“处于 S 模式的 Windows 10 指南”中所述的其他代码完整性策略。
   * 驱动程序不包含驱动程序包中的任何非 Microsoft UI 组件或应用程序。

   ![提交 Windows 10 S 驱动程序时必须选中的两个复选框的屏幕截图](images/win-cloud-checkboxes.png)

10. 选择“发布”将请求发送到 Windows 更新。 如果不希望立即发布发货标签，可选择“保存”。 以后可通过打开发货标签并选择“发布”来发布发货标签，或者可从硬件提交页面中选择“发布所有待处理”。 请注意，选择“发布所有待处理”将发布所有未发布的发货标签。

 

 

