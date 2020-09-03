---
title: DDI 用法规则集 (Storport)
description: 使用这些规则验证驱动程序正确使用 Storport DDIs。
ms.assetid: 858BBD97-4E3D-464A-B85F-358809431347
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 23f234b2f85023e69b0e6d006ba1da1fcd5224fc
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384957"
---
# <a name="ddi-usage-rule-set-storport"></a>DDI 用法规则集 (Storport)


使用这些规则验证驱动程序正确使用 Storport DDIs。

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
<td align="left"><p><a href="storport-hwstorportprohibitedddis.md" data-raw-source="[&lt;strong&gt;HwStorPortProhibitedDDIs&lt;/strong&gt;](storport-hwstorportprohibitedddis.md)"><strong>HwStorPortProhibitedDDIs</strong></a></p></td>
<td align="left"><p>此规则包含 WDM DDIs (的列表，其中包含不应在物理 StorPort 微型端口驱动程序中调用的互锁函数) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="nullchecks.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullchecks.md)"><strong>NullCheck</strong></a></p></td>
<td align="left"><p>NullCheck 规则验证驱动程序代码中的 NULL 值是否在稍后的驱动程序中未被引用。 如果满足以下任一条件，则此规则将报告缺陷：</p>
<ul>
<li>指定的值为 NULL，稍后取消引用。</li>
<li>驱动程序中有一个全局/参数，该过程在后面可能为 NULL 的情况下，在该驱动程序中有一个明确的检查，表示指针的初始值可能为 NULL。</li>
</ul>
<p>对于 NullCheck 规则冲突，最相关的代码语句在跟踪树窗格中突出显示。 有关使用报表输出的详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report" data-raw-source="[Static Driver Verifier Report](./static-driver-verifier-report.md)">静态驱动程序验证程序报表</a> 和 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/understanding-the-defect-viewer" data-raw-source="[Understanding the Trace Viewer](./understanding-the-defect-viewer.md)">了解跟踪查看器</a>。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportddisportonly.md" data-raw-source="[&lt;strong&gt;StorPortDDIsPortOnly&lt;/strong&gt;](storport-storportddisportonly.md)"><strong>StorPortDDIsPortOnly</strong></a></p></td>
<td align="left"><p>此规则包含 StorPort 仅限 DDIs 的 (的列表，其中包含不应在 StorPort 微型端口中调用的互锁函数) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportdeprecated.md" data-raw-source="[&lt;strong&gt;StorPortDeprecated&lt;/strong&gt;](storport-storportdeprecated.md)"><strong>StorPortDeprecated</strong></a></p></td>
<td align="left"><p>此规则验证驱动程序是否未调用这些弃用的例程之一： <strong>StorPortValidateRange</strong> 或 <strong>StorPortLogError</strong>。</p></td>
</tr>
</tbody>
</table>

 

**选择 DDI 使用规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 **DDIUsage**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**DDIUsage。 sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:DDIUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

 

