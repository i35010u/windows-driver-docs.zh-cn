---
title: 警告规则集 (Storport)
description: 使用这些规则来验证驱动程序是否可以在不同的上下文中正确处理 Irp，并遵循 Microsoft 推荐的最佳做法。
ms.assetid: 6557A741-C49F-456B-B285-DE6D171DDCEE
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1a0bf83194b0729728b3c6d23464387723af2761
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383571"
---
# <a name="warning-rule-set-storport"></a>警告规则集 (Storport)


使用这些规则来验证驱动程序是否可以在不同的上下文中正确处理 Irp，并遵循 Microsoft 推荐的最佳做法。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="storport-pagedcode.md" data-raw-source="[&lt;strong&gt;PagedCode&lt;/strong&gt;](storport-pagedcode.md)"><strong>PagedCode</strong></a></p></td>
<td align="left"><p>此规则验证在调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PAGED_CODE&lt;/strong&gt;](../kernel/mm-bad-pointer.md)"><strong>PAGED_CODE</strong></a> 宏时，驱动程序的 <strong> &lt; DISPATCH_LEVEL 为 IRQL</strong>。 在 <strong>IRQL &gt; = DISPATCH_LEVEL</strong> 执行的任何代码必须位于非分页内存中，以避免导致页错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportstatuspending.md" data-raw-source="[&lt;strong&gt;StorPortStatusPending&lt;/strong&gt;](storport-storportstatuspending.md)"><strong>StorPortStatusPending</strong></a></p></td>
<td align="left"><p>此规则检查 SRB 是否未完成，状态 <strong>SRB_STATUS_PENDING</strong>。</p></td>
</tr>
</tbody>
</table>

 

**选择警告规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 " **警告**"。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请指定带有 **/check**选项的**sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Warning.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

 

