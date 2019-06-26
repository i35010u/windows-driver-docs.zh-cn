---
title: DDI 用法规则集 (Storport)
description: 使用这些规则来验证您的驱动程序正确使用 Storport DDIs 正确。
ms.assetid: 858BBD97-4E3D-464A-B85F-358809431347
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4f741677a4ba4e4f79242859611b38453b1fd24d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394103"
---
# <a name="ddi-usage-rule-set-storport"></a>DDI 用法规则集 (Storport)


使用这些规则来验证您的驱动程序正确使用 Storport DDIs 正确。

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
<td align="left"><p><a href="storport-hwstorportprohibitedddis.md" data-raw-source="[&lt;strong&gt;HwStorPortProhibitedDDIs&lt;/strong&gt;](storport-hwstorportprohibitedddis.md)"><strong>HwStorPortProhibitedDDIs</strong></a></p></td>
<td align="left"><p>此规则包含一系列 WDM DDIs （不包括互锁的函数） 不应在物理 StorPort 微型端口驱动程序中调用的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="nullchecks.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullchecks.md)"><strong>NullCheck</strong></a></p></td>
<td align="left"><p>NullCheck 规则验证驱动程序代码中的 NULL 值不会取消引用驱动程序中更高版本。 如果其中一项条件为 true，此规则将报告缺陷：</p>
<ul>
<li>没有为 NULL，则取消分配更高版本。</li>
<li>一个全局/参数可能为更高版本，取消引用 NULL 的驱动程序中的过程，并且没有显式签入中建议的指针的初始值可能为 NULL 的驱动程序。</li>
</ul>
<p>与 NullCheck 规则冲突，跟踪树窗格中突出显示最相关的代码语句。 有关使用报表输出的详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report" data-raw-source="[Static Driver Verifier Report](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report)">静态驱动程序验证工具报告</a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/understanding-the-defect-viewer" data-raw-source="[Understanding the Trace Viewer](https://docs.microsoft.com/windows-hardware/drivers/devtest/understanding-the-defect-viewer)">了解跟踪查看器</a>。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportddisportonly.md" data-raw-source="[&lt;strong&gt;StorPortDDIsPortOnly&lt;/strong&gt;](storport-storportddisportonly.md)"><strong>StorPortDDIsPortOnly</strong></a></p></td>
<td align="left"><p>此规则包含 StorPort 仅端口 DDIs （不包括互锁的函数），不应调用在 StorPort 微型端口的列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportdeprecated.md" data-raw-source="[&lt;strong&gt;StorPortDeprecated&lt;/strong&gt;](storport-storportdeprecated.md)"><strong>StorPortDeprecated</strong></a></p></td>
<td align="left"><p>此规则验证，该驱动程序不会调用这些不推荐使用的例程之一：<strong>StorPortValidateRange</strong>或<strong>StorPortLogError</strong>。</p></td>
</tr>
</tbody>
</table>

 

**若要选择 DDI 使用率规则设置**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...** .

2.  单击**规则**选项卡。下**规则集**，选择**DDIUsage**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**DDIUsage.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:DDIUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)并[Static Driver Verifier 命令 (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 





