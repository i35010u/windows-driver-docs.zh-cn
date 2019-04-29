---
title: 诊断和调试
description: 诊断和调试
ms.assetid: 6c5c1b4a-338d-4550-903d-c6905ce743f9
keywords:
- RDBSS WDK 文件系统中诊断
- 重定向驱动器缓冲子系统 WDK 文件系统中诊断
- 诊断 WDK RDBSS
- 调试驱动程序 WDK RDBSS
- 驱动程序调试 WDK RDBSS
- RDBSS WDK 的文件系统调试
- 重定向驱动器缓冲子系统 WDK 的文件系统调试
- 取消引用跟踪 WDK RDBSS
- 引用跟踪 WDK RDBSS
- 断言例程 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c4af1c575bc56b9de201e8136b177787e6127cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359309"
---
# <a name="diagnostics-and-debugging"></a>诊断和调试


## <span id="ddk_diagnostics_and_debugging_if"></span><span id="DDK_DIAGNOSTICS_AND_DEBUGGING_IF"></span>


RDBSS 用于诊断和调试目的提供了大量例程。 这些例程划分为两个类别：

-   断言和调试例程

-   引用，并取消引用跟踪例程

这些例程包括下表中各项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553384" data-raw-source="[&lt;strong&gt;RxAssert&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553384)"><strong>RxAssert</strong></a></p></td>
<td align="left"><p>此例程将发送中选中的 assert 字符串生成的 RDBSS 到内核调试程序如果安装了一个。 RxAssert.h 包括时使用文件时，Windows 内核<strong>RtlAssert</strong>调用将重新定义，以将此称为<a href="https://msdn.microsoft.com/library/windows/hardware/ff553384" data-raw-source="[&lt;strong&gt;RxAssert&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553384)"> <strong>RxAssert</strong> </a>也例程。</p>
<p>对于零售版本，对此例程的调用将 bug 检查。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554385" data-raw-source="[&lt;strong&gt;RxDbgBreakPoint&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554385)"><strong>RxDbgBreakPoint</strong></a></p></td>
<td align="left"><p>此例程会引发异常，如果已安装; 由内核调试程序否则，它是由调试系统进行处理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554655" data-raw-source="[&lt;strong&gt;RxpTrackDereference&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554655)"><strong>RxpTrackDereference</strong></a></p></td>
<td align="left"><p>此例程用于跟踪请求以引用 SRV_CALL、 NET_ROOT、 V_NET_ROOT、 FOBX、 FCB，并在选中 SRV_OPEN 结构生成。 可以通过日志记录系统和 WMI 访问的这些引用请求的日志。 此例程不执行取消引用操作。</p>
<p>对于零售版本，此例程没有任何影响。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554659" data-raw-source="[&lt;strong&gt;RxpTrackReference&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554659)"><strong>RxpTrackReference</strong></a></p></td>
<td align="left"><p>此例程用于跟踪的请求，若要取消引用 SRV_CALL、 NET_ROOT、 V_NET_ROOT、 FOBX、 FCB，并在选中 SRV_OPEN 结构生成。 这些日志取消引用请求的日志记录系统和 WMI 可访问。 此例程不会执行引用操作。</p>
<p>对于零售版本，此例程没有任何影响。</p></td>
</tr>
</tbody>
</table>

 

除了上表中列出的例程，大量的宏，以调用这些例程定义以进行调试。 下表中列出的这些宏提供周围的包装器[ **RxReference** ](https://msdn.microsoft.com/library/windows/hardware/ff554688)或[ **RxDereference** ](https://msdn.microsoft.com/library/windows/hardware/ff554388)例程用于 SRV 上的文件结构管理操作\_调用时，NET\_根、 V\_NET\_根、 FOBX、 FCB 和 SRV\_打开结构。 这些宏首先调用对应[ **RxpTrackReference** ](https://msdn.microsoft.com/library/windows/hardware/ff554659)或[ **RxpTrackDereference** ](https://msdn.microsoft.com/library/windows/hardware/ff554655)例程，以记录诊断信息，然后调用相应**RxReference**或**RxDeference**例程。 一个引用的登录，并取消引用请求可由 RDBSS 日志记录系统和 WMI 访问。

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
<td align="left"><p><strong>RxDereferenceAndFinalizeNetFcb</strong> (<em>Fcb ,RxContext</em>, <em>RecursiveFinalize</em>, <em>ForceFinalize</em>)</p></td>
<td align="left"><p>使用此宏来跟踪取消引用 FCB 结构上的操作。</p>
<p>请注意，此宏操作的引用计数也会返回 finalize 调用的状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxDereferenceNetFcb</strong> (<em>Fcb</em>)</p></td>
<td align="left"><p>使用此宏来跟踪取消引用 FCB 结构上的操作。</p>
<p>请注意，此宏操作的引用计数也会返回最终的取消引用调用的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceNetFobx</strong> (<em>Fobx,LockHoldingState</em>)</p></td>
<td align="left"><p>使用此宏来跟踪取消引用 FOBX 结构上的操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxDereferenceNetRoot</strong> (<em>NetRoot</em>, <em>LockHoldingState</em>)</p></td>
<td align="left"><p>使用此宏来跟踪取消引用 NET_ROOT 结构上的操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceSrvCall</strong> (<em>SrvCall</em>, <em>LockHoldingState</em>)</p></td>
<td align="left"><p>使用此宏来跟踪取消引用 SRV_CALL 结构上的操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxDereferenceSrvOpen</strong> ( <em>SrvOpen</em>, <em>LockHoldingState</em>)</p></td>
<td align="left"><p>使用此宏来跟踪取消引用 SRV_OPEN 结构上的操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceVNetRoot</strong> ( <em>VNetRoot</em>, <em>LockHoldingState</em>)</p></td>
<td align="left"><p>使用此宏来跟踪取消引用 NET_ROOT 结构上的操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceNetFcb</strong> (<em>Fcb</em>)</p></td>
<td align="left"><p>此宏用于跟踪对 FCB 结构的引用操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceNetFobx</strong> (<em>Fobx</em>)</p></td>
<td align="left"><p>此宏用于跟踪对 FOBX 结构的引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceNetRoot</strong> (<em>NetRoot</em>)</p></td>
<td align="left"><p>此宏用于跟踪对 NET_ROOT 结构的引用操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceSrvCall</strong> (<em>SrvCall</em>)</p></td>
<td align="left"><p>此宏用于跟踪对在 DPC 级别不是 SRV_CALL 结构的引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceSrvCallAtDpc</strong> (<em>SrvCall</em>)</p></td>
<td align="left"><p>此宏用于跟踪对在 DPC 级别 SRV_CALL 结构的引用操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceSrvOpen</strong> (<em>SrvOpen</em>)</p></td>
<td align="left"><p>此宏用于跟踪对 SRV_OPEN 结构的引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceVNetRoot</strong> (<em>VNetRoot</em>)</p></td>
<td align="left"><p>此宏用于跟踪对 V_NET_ROOT 结构的引用操作。</p></td>
</tr>
</tbody>
</table>

 

 

 




