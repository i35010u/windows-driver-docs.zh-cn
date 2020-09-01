---
title: 诊断和调试
description: 诊断和调试
ms.assetid: 6c5c1b4a-338d-4550-903d-c6905ce743f9
keywords:
- RDBSS WDK 文件系统，诊断
- 重定向驱动器缓冲子系统 WDK 文件系统，诊断
- 诊断 WDK RDBSS
- 调试驱动程序 WDK RDBSS
- 驱动程序调试 WDK RDBSS
- RDBSS WDK 文件系统，调试
- 重定向驱动器缓冲子系统 WDK 文件系统，调试
- 取消引用跟踪 WDK RDBSS
- 引用跟踪 WDK RDBSS
- 断言例程 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4460dcd016d8b6a948c935d2c0a7aa871a77e789
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065336"
---
# <a name="diagnostics-and-debugging"></a>诊断和调试


## <span id="ddk_diagnostics_and_debugging_if"></span><span id="DDK_DIAGNOSTICS_AND_DEBUGGING_IF"></span>


RDBSS 提供了许多用于诊断和调试的例程。 这些例程分为两类：

-   断言和调试例程

-   引用和取消引用跟踪例程

这些例程包括下表中的项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程所返回的值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxassert" data-raw-source="[&lt;strong&gt;RxAssert&lt;/strong&gt;](./rxassert.md)"><strong>RxAssert</strong></a></p></td>
<td align="left"><p>如果安装了一个，则此例程会将 RDBSS 的已检查版本中的断言字符串发送到内核调试器。 使用 rxAssert 包含文件时，将重新定义 Windows 内核 <strong>RtlAssert</strong> 调用以调用此 <a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxassert" data-raw-source="[&lt;strong&gt;RxAssert&lt;/strong&gt;](./rxassert.md)"><strong>rxAssert</strong></a> 例程。</p>
<p>对于零售版本，调用此例程将会检查错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/rxdbgbreakpoint" data-raw-source="[&lt;strong&gt;RxDbgBreakPoint&lt;/strong&gt;](./rxdbgbreakpoint.md)"><strong>RxDbgBreakPoint</strong></a></p></td>
<td align="left"><p>如果安装了某个内核调试器，此例程会引发异常;否则，调试系统会对其进行处理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackdereference" data-raw-source="[&lt;strong&gt;RxpTrackDereference&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackdereference)"><strong>RxpTrackDereference</strong></a></p></td>
<td align="left"><p>此例程用于跟踪请求，以在检查的生成中引用 SRV_CALL、NET_ROOT、V_NET_ROOT、FOBX、FCB 和 SRV_OPEN 结构。 日志记录系统和 WMI 可访问这些引用请求的日志。 此例程不执行取消引用操作。</p>
<p>对于零售版本，此例程不执行任何操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackreference" data-raw-source="[&lt;strong&gt;RxpTrackReference&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackreference)"><strong>RxpTrackReference</strong></a></p></td>
<td align="left"><p>此例程用于跟踪在已检查生成中取消引用 SRV_CALL、NET_ROOT、V_NET_ROOT、FOBX、FCB 和 SRV_OPEN 结构的请求。 日志记录系统和 WMI 可访问这些取消引用请求的日志。 此例程不执行引用操作。</p>
<p>对于零售版本，此例程不执行任何操作。</p></td>
</tr>
</tbody>
</table>

 

除了上表中列出的例程以外，还定义了多个调用这些例程的宏用于调试。 下表中列出了这些宏，其中提供了围绕 SRV 调用、NET [**RxReference**](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxreference) [**RxDereference**](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdereference) \_ \_ ROOT、NET.TCP \_ NET \_ root、FOBX、FCB 和 SRV \_ 开放式结构的文件结构管理操作的 RxReference 或 RxDereference 例程的包装。 在调用相应的**RxReference**或**RxDeference**例程之前，这些宏首先调用相应的[**RxpTrackReference**](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackreference)或[**RxpTrackDereference**](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackdereference)例程来记录诊断信息。 RDBSS 日志记录系统和 WMI 可以访问引用和取消引用请求的日志。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">宏</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceAndFinalizeNetFcb</strong> (<em>Fcb、RxContext</em>、 <em>RecursiveFinalize</em>、 <em>ForceFinalize</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 FCB 结构的取消引用操作。</p>
<p>请注意，此宏操作引用计数，同时返回 finalize 调用的状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxDereferenceNetFcb</strong> (<em>Fcb</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 FCB 结构的取消引用操作。</p>
<p>请注意，此宏操作引用计数，同时返回最终取消引用调用的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceNetFobx</strong> (<em>Fobx，LockHoldingState</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 FOBX 结构的取消引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxDereferenceNetRoot</strong> (<em>NetRoot</em>， <em>LockHoldingState</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 NET_ROOT 结构的取消引用操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceSrvCall</strong> (<em>SrvCall</em>， <em>LockHoldingState</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 SRV_CALL 结构的取消引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxDereferenceSrvOpen</strong> ( <em>SrvOpen</em>， <em>LockHoldingState</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 SRV_OPEN 结构的取消引用操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceVNetRoot</strong> ( <em>VNetRoot</em>， <em>LockHoldingState</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 NET_ROOT 结构的取消引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceNetFcb</strong> (<em>Fcb</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 FCB 结构的引用操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceNetFobx</strong> (<em>Fobx</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 FOBX 结构的引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceNetRoot</strong> (<em>NetRoot</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 NET_ROOT 结构的引用操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceSrvCall</strong> (<em>SrvCall</em>) </p></td>
<td align="left"><p>此宏用于跟踪对不在 DPC 级别 SRV_CALL 结构的引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceSrvCallAtDpc</strong> (<em>SrvCall</em>) </p></td>
<td align="left"><p>此宏用于在 DPC 级别跟踪对 SRV_CALL 结构的引用操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceSrvOpen</strong> (<em>SrvOpen</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 SRV_OPEN 结构的引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceVNetRoot</strong> (<em>VNetRoot</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 V_NET_ROOT 结构的引用操作。</p></td>
</tr>
</tbody>
</table>

 

 

