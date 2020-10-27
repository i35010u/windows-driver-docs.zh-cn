---
title: 将驱动程序发布到 Windows 更新
description: 若要将驱动程序发布到 Windows 更新，请创建硬件提交，然后按照下面的步骤操作。
ms.assetid: E62AADCF-E481-40CA-98F1-BE4629C3EE35
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c71050c56e66c7264360c824c6c50d157fef9f90
ms.sourcegitcommit: c94be6fc464edc94035060a4723efa06ab0f5af9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/17/2020
ms.locfileid: "92153479"
---
# <a name="publish-a-driver-to-windows-update"></a>将驱动程序发布到 Windows 更新


若要将驱动程序发布到 Windows 更新，请[创建硬件提交](create-a-new-hardware-submission.md)，然后按照下面的步骤操作。

1. [查找硬件提交](manage-your-hardware-submissions.md)，该提交中包含你想要分发的驱动程序。

2. 转到硬件提交的“分配”  部分，然后选择“新发货标签”  。

   ![显示“新建发货标签”按钮的屏幕截图](images/publish-new-shipping-label.png)

3. 在发货标签页面上，转到“详细信息”  部分，然后在“发货标签名称”  字段中输入发货标签的名称。 此名称允许你组织和搜索发货标签。

4. 在“属性”  部分中，完成以下信息：

|字段|说明|
|--- |--- |
|**目标**|选择“发布到 Windows 更新”将驱动程序发布到 Windows 更新。 如果要创建允许你与合作伙伴共享驱动程序的共享发货标签，请参阅[与合作伙伴共享驱动程序](sharing-drivers-with-your-partners.md)。 **注意** 共享驱动程序只能由最初创建它的组织共享。 接收共享驱动程序的组织无法再次共享它。|
|**指定合作伙伴（如果有），使其获得对此请求的可见性**|输入希望其具有驱动程序和发货标签的只读权限的合作伙伴。 希望合作伙伴注意此发货标签请求时（例如当代表他们发布驱动程序时），使用此字段。 有关详细信息，请参阅[代表合作伙伴发布驱动程序](/previous-versions/mt786462(v=vs.85))。|
|**驱动程序交付选项**|目标为 Windows 更新时，默认选项为“自动”，这意味着在升级时，驱动程序会自动交付到每个适用的系统。 如果你只选择“在 Windows 升级过程中自动交付”，则驱动程序将定义为动态驱动程序，并仅在操作系统升级期间交付。 如果你只选择“自动交付到所有适用系统”，则在驱动程序发布后，Windows 更新会立即将驱动程序交付给所有适用的系统。<br/><br/>如果在 Windows 10 版本 1909 或更低版本中选择“手动”，则仅当设备上未安装驱动程序或只有通用驱动程序时，才会自动交付驱动程序。<br/><br/>从 Windows 10 版本 2004 开始，系统不会自动交付带有“手动”发货标签的驱动程序。 若要访问最佳匹配“可选/手动”驱动程序，用户必须转到“设置”>“更新和安全”>“Windows 更新”>“查看可选更新”>“驱动程序更新” 。|

![显示标签名称和发布属性的屏幕截图](images/label-name-and-properties-windows-update.png)

5. 在“目标”  部分中，选择要发布的驱动程序包。

6. 选择驱动程序包后，“选择 PNP”  变为可用。 选择要面向的硬件 ID。 可使用硬件 ID 列表上方的搜索框搜索特定硬件 ID 或操作系统。

   若要面向所有列出的硬件 ID，请选择“全部发布”  。

   若要面向特定硬件 ID，请查找每个所需的硬件 ID，然后选择“发布”  。

   如果曾面向所有硬件 ID，但现在希望删除它们，请选择“全部过期”  。

   若要删除对特定硬件 ID 的目标设定，请查找每个硬件 ID，然后选择“过期”  。

   ![显示目标部分和 PNP 的屏幕截图](images/publish-targeting-windows-update.png)

7. 如果要添加计算机硬件 ID (CHID)，请在文本框中输入每个 CHID，然后选择“添加 CHID”  。 若要批量添加多个 CHID，请确保每个 CHID 都由换行符分隔、选择“添加多个 CHID”  ，然后将 CHID 粘贴到文本框。 可在文本框下方的列表中查看所有添加的 CHID。 若要从列表中删除 CHID，请选择“删除” 

>[!IMPORTANT]
> 以下 Windows 版本不支持 CHID：
> * Windows 8.1 或更低版本
> * Windows Server 2012 R2 或更低版本
>
> 如果你的驱动程序面向这些操作系统中的任何一个，请创建两个发货标签：一个用于 Windows 10（可以在其中添加 CHID），另一个用于低级别操作系统（不会在其中添加 CHID）。



8. 如果你希望限制在 Windows 更新目录和 WSUS 目录中公开披露你的发货标签，请选中“限制此发货标签信息的公开披露”  。 box.  

   ![显示限制公开披露的屏幕截图](images/limit-public-disclosure.PNG)

   你的驱动程序仍然可以从 Windows 更新发布和下载，但不会显示在任何公共目录列表中。

9. 如果驱动程序面向处于 S 模式的 Windows 10，则必须将两个框都选中，并确认满足以下条件：

   * 驱动程序兼容且遵循[处于 S 模式的 Windows 10 驱动程序要求](../install/windows10sdriverrequirements.md)中所述的驱动程序策略。
   * 确保驱动程序遵循“处于 S 模式的 Windows 10 指南”中所述的其他代码完整性策略。
   * 驱动程序不包含驱动程序包中的任何非 Microsoft UI 组件或应用程序。

   ![提交 Windows 10 S 驱动程序时必须选中的两个复选框的屏幕截图](images/win-cloud-checkboxes.png)

10. 选择“发布”  将请求发送到 Windows 更新。 如果不希望立即发布发货标签，可选择“保存”  。 以后可通过打开发货标签并选择“发布”  来发布发货标签，或者可从硬件提交页面中选择“发布所有待处理”  。 请注意，选择“发布所有待处理”  将发布所有未发布的发货标签。

