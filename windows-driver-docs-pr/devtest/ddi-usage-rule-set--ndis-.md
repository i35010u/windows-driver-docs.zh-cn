---
title: DDI 使用规则集 (NDIS)
description: 使用这些规则来验证您的驱动程序正确使用 NDIS DDIs 正确。
ms.assetid: A109A452-D3A7-4204-B267-1F0F98652597
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: b6f876d189f9c83e274e16591aade6694eb24a3c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519214"
---
# <a name="ddi-usage-rule-set-ndis"></a>DDI 使用规则集 (NDIS)


使用这些规则来验证您的驱动程序正确使用 NDIS DDIs 正确。

## <a name="in-this-section"></a>本部分内容


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
<td align="left"><p><a href="ndis-init-deregisterinterrupt.md" data-raw-source="[&lt;strong&gt;Init_DeRegisterInterrupt&lt;/strong&gt;](ndis-init-deregisterinterrupt.md)"><strong>Init_DeRegisterInterrupt</strong></a></p></td>
<td align="left"><p><a href="ndis-init-deregisterinterrupt.md" data-raw-source="[&lt;strong&gt;Init_DeRegisterInterrupt&lt;/strong&gt;](ndis-init-deregisterinterrupt.md)"> <strong>Init_DeRegisterInterrupt</strong> </a>规则指定，如果<a href="https://msdn.microsoft.com/library/windows/hardware/ff563649" data-raw-source="[&lt;strong&gt;NdisMRegisterInterruptEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563649)"> <strong>NdisMRegisterInterruptEx</strong> </a>至少一次期间调用MPInitilize， <a href="https://msdn.microsoft.com/library/windows/hardware/ff563575" data-raw-source="[&lt;strong&gt;NdisMDeregisterInterruptEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563575)"> <strong>NdisMDeregisterInterruptEx</strong> </a> MPHaltEx 应至少一次调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-init-ndisallocateioworkitem.md" data-raw-source="[&lt;strong&gt;Init_NdisAllocateIoWorkItem&lt;/strong&gt;](ndis-init-ndisallocateioworkitem.md)"><strong>Init_NdisAllocateIoWorkItem</strong></a></p></td>
<td align="left"><p><a href="ndis-init-ndisallocateioworkitem.md" data-raw-source="[&lt;strong&gt;Init_NdisAllocateIoWorkItem&lt;/strong&gt;](ndis-init-ndisallocateioworkitem.md)"> <strong>Init_NdisAllocateIoWorkItem</strong> </a>规则指定，如果<a href="https://msdn.microsoft.com/library/windows/hardware/ff561604" data-raw-source="[&lt;strong&gt;NdisAllocateIoWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561604)"> <strong>NdisAllocateIoWorkItem</strong> </a>期间至少一次调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff559389" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559389)"><em>MiniportInitializeEx</em></a>，则<a href="https://msdn.microsoft.com/library/windows/hardware/ff561855" data-raw-source="[&lt;strong&gt;NdisFreeIoWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561855)"> <strong>NdisFreeIoWorkItem</strong> </a>函数应：</p>
<ul>
<li>- 如果在 MPHaltEx，至少一次调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff559389" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559389)"> <em>MiniportInitializeEx</em> </a>成功。</li>
<li>- 在中调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff559389" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559389)"> <em>MiniportInitializeEx</em></a>，如果<em>MiniportInitializeEx</em>失败。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-init-registerinterrupt.md" data-raw-source="[&lt;strong&gt;Init_RegisterInterrupt&lt;/strong&gt;](ndis-init-registerinterrupt.md)"><strong>Init_RegisterInterrupt</strong></a></p></td>
<td align="left"><p>Init_RegisterInterrupt 规则指定，是否出现问题或过程停止微型端口驱动程序初始化过程中，注册中断，这通常发生在初始化期间，必须是撤消。</p>
<p>如果<strong>NdisMRegisterInterruptEx</strong>称为至少一次<strong>MiniportInitializeEx</strong>，则<strong>NdisMDeregisterInterruptEx</strong>必须至少一次调用函数在中<strong>MiniportHaltEx</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-init-registersg.md" data-raw-source="[&lt;strong&gt;Init_RegisterSG&lt;/strong&gt;](ndis-init-registersg.md)"><strong>Init_RegisterSG</strong></a></p></td>
<td align="left"><p>Init_RegisterSG 规则指定，是否出现问题或过程停止微型端口驱动程序初始化过程中，通常发生在初始化期间，分散-集中列表 (SG) 的注册必须被撤消。</p>
<p>如果<strong>NdisMRegisterScatterGatherDma</strong>称为至少一次<strong>MiniportInitializeEx</strong>，则<strong>NdisMDeregisterScatterGatherDma</strong>必须在调用函数中的至少一次<strong>MiniportHaltEx</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisfderegisterfilterdriver.md" data-raw-source="[&lt;strong&gt;NdisFDeregisterFilterDriver&lt;/strong&gt;](ndis-ndisfderegisterfilterdriver.md)"><strong>NdisFDeregisterFilterDriver</strong></a></p></td>
<td align="left"><p>筛选器驱动程序必须调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff561800" data-raw-source="[&lt;strong&gt;NdisFDeregisterFilterDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561800)"> <strong>NdisFDeregisterFilterDriver</strong> </a>从其<a href="https://msdn.microsoft.com/library/windows/hardware/ff549936" data-raw-source="[&lt;strong&gt;FilterDriverUnload&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549936)"> <strong>FilterDriverUnload</strong> </a>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndismderegisterinterruptex.md" data-raw-source="[&lt;strong&gt;NdisMDeregisterInterruptEx&lt;/strong&gt;](ndis-ndismderegisterinterruptex.md)"><strong>NdisMDeregisterInterruptEx</strong></a></p></td>
<td align="left"><p>之后<a href="https://msdn.microsoft.com/library/windows/hardware/ff563575" data-raw-source="[&lt;strong&gt;NdisMDeregisterInterruptEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563575)"> <strong>NdisMDeregisterInterruptEx</strong> </a>返回控件，微型端口驱动程序不能调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff563681" data-raw-source="[&lt;strong&gt;NdisMSynchronizeWithInterruptEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563681)"> <strong>NdisMSynchronizeWithInterruptEx</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="nullcheckn.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullcheckn.md)"><strong>NullCheck</strong></a></p></td>
<td align="left"><p>NullCheck 规则验证驱动程序代码中的 NULL 值不会取消引用驱动程序中更高版本。 如果其中一项条件为 true，此规则将报告缺陷：</p>
<ul>
<li>没有为 NULL，则取消分配更高版本。</li>
<li>一个全局/参数可能为更高版本，取消引用 NULL 的驱动程序中的过程，并且没有显式签入中建议的指针的初始值可能为 NULL 的驱动程序。</li>
</ul>
<p>与 NullCheck 规则冲突，跟踪树窗格中突出显示最相关的代码语句。 有关使用报表输出的详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff552834" data-raw-source="[Static Driver Verifier Report](https://msdn.microsoft.com/library/windows/hardware/ff552834)">静态驱动程序验证工具报告</a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff554020" data-raw-source="[Understanding the Trace Viewer](https://msdn.microsoft.com/library/windows/hardware/ff554020)">了解跟踪查看器</a>。</p>
<p></p></td>
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

 

 





