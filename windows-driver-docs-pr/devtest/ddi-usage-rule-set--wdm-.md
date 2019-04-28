---
title: DDI 用法规则集 (WDM)
description: 使用这些规则来验证您的驱动程序正确使用 WDM DDIs 正确。
ms.assetid: B958191C-8E14-4D4D-9D0F-AD5D29599E53
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: bcd9d30290931adf48098bd49489f092e7fe1e12
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327117"
---
# <a name="ddi-usage-rule-set-wdm"></a>DDI 用法规则集 (WDM)


使用这些规则来验证您的驱动程序正确使用 WDM DDIs 正确。

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
<td align="left"><p><a href="wdm-debugbreakusage.md" data-raw-source="[&lt;strong&gt;DebugBreakUsage&lt;/strong&gt;](wdm-debugbreakusage.md)"><strong>DebugBreakUsage</strong></a></p></td>
<td align="left"><p><a href="wdm-debugbreakusage.md" data-raw-source="[&lt;strong&gt;DebugBreakUsage&lt;/strong&gt;](wdm-debugbreakusage.md)"> <strong>DebugBreakUsage</strong> </a>规则指定驱动程序必须调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff543626" data-raw-source="[&lt;strong&gt;DbgBreakPoint&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543626)"> <strong>DbgBreakPoint</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff543629" data-raw-source="[&lt;strong&gt;DbgBreakPointWithStatus&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543629)"> <strong>DbgBreakPointWithStatus</strong></a>。 要生成非调试版本的驱动程序，则仅适用于此规则。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="nullcheckw.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullcheckw.md)"><strong>NullCheck</strong></a></p></td>
<td align="left"><p>NullCheck 规则验证驱动程序代码中的 NULL 值不会取消引用驱动程序中更高版本。 如果其中一项条件为 true，此规则将报告缺陷：</p>
<ul>
<li>没有为 NULL，则取消分配更高版本。</li>
<li>一个全局/参数可能为更高版本，取消引用 NULL 的驱动程序中的过程，并且没有显式签入中建议的指针的初始值可能为 NULL 的驱动程序。</li>
</ul>
<p>与 NullCheck 规则冲突，跟踪树窗格中突出显示最相关的代码语句。 有关使用报表输出的详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff552834" data-raw-source="[Static Driver Verifier Report](https://msdn.microsoft.com/library/windows/hardware/ff552834)">静态驱动程序验证工具报告</a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff554020" data-raw-source="[Understanding the Trace Viewer](https://msdn.microsoft.com/library/windows/hardware/ff554020)">了解跟踪查看器</a>。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-safestrings.md" data-raw-source="[&lt;strong&gt;SafeStrings&lt;/strong&gt;](wdm-safestrings.md)"><strong>SafeStrings</strong></a></p></td>
<td align="left"><p><a href="wdm-safestrings.md" data-raw-source="[&lt;strong&gt;SafeStrings&lt;/strong&gt;](wdm-safestrings.md)"> <strong>SafeStrings</strong> </a>规则指定驱动程序调用仅保护系统免受无意或恶意入侵这些字符串操作函数。 驱动程序这些安全的字符串函数 Ntstrsafe.h 中定义。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-obsoleteddis.md" data-raw-source="[&lt;strong&gt;ObsoleteDDIs&lt;/strong&gt;](wdm-obsoleteddis.md)"><strong>ObsoleteDDIs</strong></a></p></td>
<td align="left"><p><a href="wdm-obsoleteddis.md" data-raw-source="[&lt;strong&gt;ObsoleteDDIs&lt;/strong&gt;](wdm-obsoleteddis.md)"> <strong>ObsoleteDDIs</strong> </a>规则指定驱动程序不应调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff547164" data-raw-source="[&lt;strong&gt;FsRtlPrivateLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547164)"> <strong>FsRtlPrivateLock</strong></a>。 此函数已过时。 使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545940" data-raw-source="[&lt;strong&gt;FsRtlFastLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545940)"> <strong>FsRtlFastLock</strong> </a>相反。</p></td>
</tr>
</tbody>
</table>

 

**若要选择 DDI 使用率规则设置**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...**.

2.  单击**规则**选项卡。下**规则集**，选择**DDIUsage**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**DDIUsage.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:DDIUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/hh454281)并[Static Driver Verifier 命令 (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)。

 

 





