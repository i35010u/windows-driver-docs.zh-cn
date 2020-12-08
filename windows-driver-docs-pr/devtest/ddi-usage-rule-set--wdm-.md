---
title: DDI 用法规则集 (WDM)
description: 使用这些规则验证驱动程序正确使用 WDM DDIs。
ms.date: 10/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: ff0e4e8d7f773985b2fdac9641859c513cf052ec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824261"
---
# <a name="ddi-usage-rule-set-wdm"></a>DDI 用法规则集 (WDM)


使用这些规则验证驱动程序正确使用 WDM DDIs。

## <a name="in-this-section"></a>在本节中


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
<td align="left"><p><a href="wdm-debugbreakusage.md" data-raw-source="[&lt;strong&gt;DebugBreakUsage&lt;/strong&gt;](wdm-debugbreakusage.md)"><strong>DebugBreakUsage</strong></a>规则指定驱动程序不得调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpoint" data-raw-source="[&lt;strong&gt;DbgBreakPoint&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpoint)"><strong>DbgBreakPoint</strong></a>或<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpointwithstatus" data-raw-source="[&lt;strong&gt;DbgBreakPointWithStatus&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgbreakpointwithstatus)"><strong>DbgBreakPointWithStatus</strong></a>。 仅当构建驱动程序的非调试版本时，此规则才适用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-doublefetch.md" data-raw-source="[&lt;strong&gt;DoubleFetch&lt;/strong&gt;](wdm-doublefetch.md)"><strong>DoubleFetch</strong></a></p></td>
<td align="left"><p><a href="wdm-doublefetch.md" data-raw-source="[&lt;strong&gt;DoubleFetch&lt;/strong&gt;](wdm-doublefetch.md)"><strong>DoubleFetch</strong></a>规则检查是否从用户模式内存指针进行双重提取。 用户模式内存的双内核模式访问可能导致争用条件安全问题。 访问用户模式数据时，内核模式代码需要在本地创建用户模式数据的副本，并避免多次访问用户模式数据。 否则，会导致一种称为 "双重提取" 的问题，在首次访问数据后，数据可能会发生更改。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="nullcheckw.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullcheckw.md)"><strong>NullCheck</strong></a></p></td>
<td align="left"><p><a href="nullcheckw.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullcheckw.md)"><strong>NullCheck</strong></a>规则验证驱动程序代码中的 NULL 值是否在稍后的驱动程序中未被引用。 如果满足以下任一条件，则此规则将报告缺陷：</p>
<ul>
<li>指定的值为 NULL，稍后取消引用。</li>
<li>驱动程序中有一个全局/参数，该过程在后面可能为 NULL 的情况下，在该驱动程序中有一个明确的检查，表示指针的初始值可能为 NULL。</li>
</ul>
<p>对于 NullCheck 规则冲突，最相关的代码语句在跟踪树窗格中突出显示。 有关使用报表输出的详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/static-driver-verifier-report" data-raw-source="[Static Driver Verifier Report](./static-driver-verifier-report.md)">静态驱动程序验证程序报表</a> 和 <a href="/windows-hardware/drivers/devtest/understanding-the-defect-viewer" data-raw-source="[Understanding the Trace Viewer](./understanding-the-defect-viewer.md)">了解跟踪查看器</a>。</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-safestrings.md" data-raw-source="[&lt;strong&gt;SafeStrings&lt;/strong&gt;](wdm-safestrings.md)"><strong>SafeStrings</strong></a></p></td>
<td align="left"><p><a href="wdm-safestrings.md" data-raw-source="[&lt;strong&gt;SafeStrings&lt;/strong&gt;](wdm-safestrings.md)"><strong>SafeStrings</strong></a>规则指定驱动程序只调用那些保护系统免受无意或恶意入侵的字符串操作函数。 驱动程序的这些安全字符串函数是在 Ntstrsafe.h 而中定义的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-obsoleteddis.md" data-raw-source="[&lt;strong&gt;ObsoleteDDIs&lt;/strong&gt;](wdm-obsoleteddis.md)"><strong>ObsoleteDDIs</strong></a></p></td>
<td align="left"><p><a href="wdm-obsoleteddis.md" data-raw-source="[&lt;strong&gt;ObsoleteDDIs&lt;/strong&gt;](wdm-obsoleteddis.md)"><strong>ObsoleteDDIs</strong></a>规则指定驱动程序不应调用<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprivatelock" data-raw-source="[&lt;strong&gt;FsRtlPrivateLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlprivatelock)"><strong>FsRtlPrivateLock</strong></a>。 此函数已过时。 改用 <a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlfastlock" data-raw-source="[&lt;strong&gt;FsRtlFastLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlfastlock)"><strong>FsRtlFastLock</strong></a> 。</p></td>
</tr>
</tbody>
</table>

 

**选择 DDI 使用规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 **DDIUsage**。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check** 选项指定 **DDIUsage。 sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:DDIUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

