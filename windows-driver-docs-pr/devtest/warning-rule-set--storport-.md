---
title: 警告规则集 (Storport)
description: 使用这些规则来验证您的驱动程序可以正确地处理 Irp，各种上下文中，如下所示，Microsoft 建议的最佳实践。
ms.assetid: 6557A741-C49F-456B-B285-DE6D171DDCEE
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 90c6e93119e5230ac4cabbb3a1e8255c8e990ed1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380469"
---
# <a name="warning-rule-set-storport"></a>警告规则集 (Storport)


使用这些规则来验证您的驱动程序可以正确地处理 Irp，各种上下文中，如下所示，Microsoft 建议的最佳实践。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="storport-pagedcode.md" data-raw-source="[&lt;strong&gt;PagedCode&lt;/strong&gt;](storport-pagedcode.md)"><strong>PagedCode</strong></a></p></td>
<td align="left"><p>此规则验证，当<a href="https://msdn.microsoft.com/library/windows/hardware/ff558773" data-raw-source="[&lt;strong&gt;PAGED_CODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558773)"> <strong>PAGED_CODE</strong> </a>调用宏，该驱动程序位于<strong>IRQL &lt; DISPATCH_LEVEL</strong>。 在执行任何代码<strong>IRQL &gt;= DISPATCH_LEVEL</strong>必须采用非分页内存，以避免导致页错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportstatuspending.md" data-raw-source="[&lt;strong&gt;StorPortStatusPending&lt;/strong&gt;](storport-storportstatuspending.md)"><strong>StorPortStatusPending</strong></a></p></td>
<td align="left"><p>此规则检查 SRB 未完成，状态<strong>SRB_STATUS_PENDING</strong>。</p></td>
</tr>
</tbody>
</table>

 

**若要选择警告规则集**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...**.

2.  单击**规则**选项卡。下**规则集**，选择**警告**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**Warning.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Warning.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/hh454281)并[Static Driver Verifier 命令 (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)。

 

 





