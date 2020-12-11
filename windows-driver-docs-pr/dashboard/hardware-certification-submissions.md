---
title: 硬件提交
description: 硬件提交
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8477e790e90d7296c727cc853444b84ecb809bff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800363"
---
# <a name="hardware-submissions"></a>硬件提交

Windows 硬件兼容性计划（适用于 Windows 10）和 Windows 硬件认证计划（适用于 Windows 8/8.1 及较早版本的操作系统）使你可以在通过合作伙伴中心提交最终版本之前，设计、创建和测试你的硬件和驱动程序。 有关详细信息，请参阅 [Windows 硬件认证](/previous-versions/windows/hardware/hck/jj124227(v=vs.85))页。 通过为 Windows 认证你的硬件设备、系统和驱动程序，你将以下列形式获得 Microsoft 市场营销资源支持：兼容性和可靠性列表、徽标图片和促销伙伴关系。

若要开发你的设备，请下载 [Windows 驱动程序工具包 (WDK)](../download-the-wdk.md)。

若要测试你的设备，请下载适用于 Windows 10 的 [Windows Hardware Lab Kit (Windows HLK)](/windows-hardware/test/hlk/windows-hardware-lab-kit)。

在开发并测试你的产品后，可以通过硬件提交的方式提交结果。

> [!NOTE]
> 我们强烈建议你将公共驱动程序符号作为 HLK 程序包的一部分包括在内。 请参阅[公共符号和私有符号](../devtest/public-symbols-and-private-symbols.md)，了解如何创建公共符号。  请参阅[步骤 8：创建提交包](/windows-hardware/test/hlk/getstarted/step-8-create-a-submission-package)，了解如何将符号包括在程序包中。 请注意，提交中的任何 .pdb 文件都将在发布前被删除。

- 若要提交 HLK 或 HCK 包，请参阅[创建新的硬件提交](create-a-new-hardware-submission.md)。

- 若要提交 WLK 包，请参阅[创建新的 WLK 设备认证提交](create-a-new-hardware-logo-submission.md)以了解详细信息。

## <a name="drivers-summary-page"></a>驱动程序摘要页

驱动程序摘要页中包含了你已创建或与你共享的所有硬件认证提交的列表。 通过选择“创建新的驱动程序”  按钮可以创建新的硬件提交。

![显示驱动程序摘要页的屏幕截图](images/drivers-summary-page.png)

硬件认证提交列表显示了每个提交的以下相关信息：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>列</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ID</strong></p></td>
<td><p>驱动程序的 ID。</p></td>
</tr>
<tr class="even">
<td><p><strong>名称</strong></p></td>
<td><p>提交创建过程中，在“驱动程序名称”中指定的名称。</p></td>
</tr>
<tr class="odd">
<td><p><strong>状态</strong></p></td>
<td><p>提交的当前状态。 可能的值为：</p>
<ul>
<li>程序包验收：提交程序包已通过正确格式和内容的初步审查。</li>
<li>准备：我们正准备对程序包进行进一步的审查和签名。</li>
<li>验证：我们正对程序包验证策略合规性和技术上的正确性。</li>
<li>手动审查：我们无法自动验证程序包内容，因此 Microsoft 员工需要费时仔细查看。</li>
<li>目录创建：我们正在为驱动程序创建安全目录。</li>
<li>签名：我们正在将 Microsoft 的签名应用到你的安全目录和二进制文件。</li>
<li>完成：我们已完成所有步骤，你的驱动程序即将准备好。</li>
<li>已完成：你的提交已完成。</li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>认证类型</strong></p></td>
<td><p>提交的认证类型。 这可以为 HLK 或 HCK。</p></td>
</tr>
<tr class="odd">
<td><p><strong>创建日期</strong></p></td>
<td><p>由你本人或与你共享驱动程序的其他人将驱动程序添加到你的帐户的日期。</p></td>
</tr>
<tr class="even">
<td><p><strong>权限</strong></p></td>
<td><p>提交的权限。 可能的值为：</p>
<ul>
<li>作者：驱动程序的作者。 可以完成所有任务，然后与合作伙伴共享该驱动程序。</li>
<li>发布者：将与你共享驱动程序。 可以下载驱动程序、创建 Windows 更新发货标签和创建 DUA 包。 不能与其他公司共享驱动程序。</li>
<li>只读：驱动程序已以你的名义提交到 Windows 更新。 可以查看驱动程序详细信息、下载驱动程序和查看以你的名义提交的发货标签。 不能创建发货标签或创建 DUA 包。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>源</strong></p></td>
<td><p>提交的作者（显示为组织名称）。</p></td>
</tr>
</tbody>
</table>

搜索框使你可以搜索特定提交或一组提交。 可以搜索“ID”  、“名称”  、“状态”  和“认证类型”  列中精确匹配或部分匹配的值。

## <a name="hardware-submission-page"></a>硬件提交页

硬件提交页中包含了有关特定硬件提交的信息，其中包括状态、程序包、认证信息和发货标签。 有关如何创建硬件提交的信息，请参阅[创建新的硬件提交](create-a-new-hardware-submission.md)。

![显示硬件提交页的屏幕截图](images/hardware-submission-page.png)

该页面的左侧部分中包含了 10 个最近查看过的提交列表。

可以通过页面顶部的进度跟踪器监视提交的进度。 所有步骤都显示绿色打勾标记后，表示提交已完成，贵公司会收到通知。

### <a name="packages-and-signing-properties"></a>程序包和签名属性

本部分介绍如何管理程序包。

若要上传新的程序包，请选择“上载新增”  。

若要下载 DUA Shell 程序包，请选择“下载 DUA Shell”  。 有关如何使用 DUA 更新提交的信息，请参阅[管理硬件提交](manage-your-hardware-submissions.md)。

已上传程序包列表中显示了该提交的已上传程序包。 选择要用于展开程序包的插入记号。 这会向你显示提交 ID，并允许你选择“下载程序包”  来下载相应程序包。

**其他认证** 显示已选择的任何其他认证。

### <a name="certification"></a>认证

本部分中显示了认证信息。 选择“查看更多信息”  可展开本部分。 可以检查你提供的认证信息，其中包括：

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
<tr class="even">
<td><p>已进行 Retpoline 编译</p></td>
<td><p>指示驱动程序是否已使用 Retpoline 标记进行编译。  勾号为 True，叉号为 False。  有关此变更的详细信息，请查看我们的<a href="https://techcommunity.microsoft.com/t5/Hardware-Dev-Center/Upcoming-Hardware-Dev-Center-changes-that-enable-support-for/ba-p/504574">博客文章</a>。 </p></td>
</tr><tr class="even">
<td><p>这是一个通用 Windows 驱动程序吗？</p></td>
<td><p>指示你的驱动程序是否满足通用 Windows 平台要求。 有关详细信息，请参阅<a href="/windows-hardware/drivers/develop/getting-started-with-universal-drivers" data-raw-source="[Getting Started with Universal Windows drivers](../develop/getting-started-with-windows-drivers.md)">通用 Windows 驱动程序入门</a>。</p></td>
</tr>
<tr class="even">
<td><p>设备属于何种类型？</p></td>
<td><p>指示你的设备是：</p>
<ul>
<li><p>内部组件，如果你的设备属于系统的一部分并连接到电脑内。</p></li>
<li><p>外部组件，如果你的设备是连接到电脑的外部设备（外设）。</p></li>
<li><p>两者，如果你的设备同时可以内部（在电脑内）和外部（外设）连接。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>选择元数据类别</p></td>
<td><p>已选择的设备元数据类别。</p>
<p>必要时可以生成一个 Sysdev 引用 ID，以便使用该 ID 将开发人员中心硬件提交与 Sysdev 设备元数据提交相关联。</p></td>
</tr>
<tr class="even">
<td><p>公布日期</p></td>
<td><p>想要将你的产品包含在 Windows Server 目录、Windows 认证产品列表和通用驱动程序列表中的日期。 默认设置是“今天”。</p></td>
</tr>
<tr class="odd">
<td><p>市场营销名称</p></td>
<td><p>你的市场营销名称。 市场营销名称允许你为产品提供别名。 你可以提供多个所需名称。</p></td>
</tr>
</tbody>
</table>

系统会根据整个提交内容为提交自动分配 Declarative 和 Universal 属性。  如果你想要将提交标记为 `Declarative=True` 和/或 `Universal=True`，则提交中的所有文件和 INF 都必须与相应的属性兼容。  例如，合并的 HLK 程序包可能包含用于不同 OS 认证的两个驱动程序集。 如果一个集是 Declarative，另一个集不是，则整个提交将标记为 `Declarative=False`。 只包含 INF 的包会普遍灰显，因为没有可验证的二进制文件。  每个集都应分入到两个提交中以确保适当地标记提交。 

如果想要添加或更新公布日期，请使用“公布日期 (UTC)”  字段并选择“提交”  。

还可以添加或删除市场营销名称。 若要添加名称，请在“市场营销名称”  文本框中输入该名称，然后选择“添加”  。 若要删除名称，请选择想要删除市场营销名称旁边的红色“X”按钮。 通过选择“添加多个名称”  还可以一次添加多个名称。 完成后，选择“提交”  。

### <a name="distribution"></a>分发

本部分中显示了此提交的发货标签信息。 有关如何使用发货标签的信息，请参阅[使用发货标签管理驱动程序分发](manage-driver-distribution-by-submission.md)部分。

选择“新建发货标签”  可创建一个新的发货标签。

选择“发布所有待处理项”  可发布所有尚未发布的发货标签。

发货标签列表中显示了该提交的发货标签。 该列表中包含了你创建的发货标签以及你的共享驱动程序的合作伙伴发货标签。 选择发货标签名称可查看该发货标签的详细信息。 发货标签列表中显示了每个标签的以下相关信息：

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
<td><p>名称</p></td>
<td><p>发货标签名称。 选择此名称可查看该发货标签的详细信息。</p></td>
</tr>
<tr class="even">
<td><p>创建者</p></td>
<td><p>发货标签创建者的“发布者显示名称”。 这使你可以轻松地跟踪哪些业务合作伙伴向你发送了驱动程序。</p></td>
</tr>
<tr class="odd">
<td><p>目标</p></td>
<td><p>对于 Windows 更新发货标签，目标为“Windows 更新”。</p>
<p>对于共享驱动程序，目标为你在创建发货标签时为“谁要发布？”所选的公司的“发布者显示名称”。 这使你可以轻松地查看共享你的驱动程序的所有公司。</p></td>
</tr>
<tr class="even">
<td><p>创建日期</p></td>
<td><p>发货标签的创建日期。</p></td>
</tr>
<tr class="odd">
<td><p>发布日期</p></td>
<td><p>发货标签的发布日期。</p></td>
</tr>
<tr class="even">
<td><p>创建者用户</p></td>
<td><p>如果发货标签由贵公司创建，你会看到创建该发货标签的用户的详细信息。 如果你对创建有疑问，这可以使你进行跟踪。 如果其他公司创建了该标签，则此字段不可用。</p></td>
</tr>
<tr class="odd">
<td><p>更改者用户</p></td>
<td><p>如果发货标签由贵公司创建，你会看到上次修改该发货标签的用户的详细信息。 如果你对更改有疑问，这可以使你进行跟踪。 如果其他公司创建了该标签，则此字段不可用。</p></td>
</tr>
</tbody>
</table>

状态图显示了每个发货标签的发布状态。 绿色打勾标记表示标签已发布。 黄色圆圈标记表示标签尚未发布。

## <a name="in-this-section"></a>本部分内容

- [创建新硬件提交](create-a-new-hardware-submission.md)

- [管理硬件提交](manage-your-hardware-submissions.md)
