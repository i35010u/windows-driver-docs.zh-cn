---
title: 定义由 RDBSS 宏
description: 定义由 RDBSS 宏
ms.assetid: 11add885-ecd9-4b43-be42-ef060e847183
keywords:
- RDBSS WDK 的文件系统宏
- 重定向驱动器缓冲子系统 WDK 的文件系统宏
- WDK RDBSS 宏
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fce4743163abccf2f355daddbce6eaa7aed9812a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545174"
---
# <a name="macros-defined-by-rdbss"></a>定义由 RDBSS 宏


## <span id="ddk_macros_defined_by_rdbss_if"></span><span id="DDK_MACROS_DEFINED_BY_RDBSS_IF"></span>


调用这些 RDBSS 例程或其他内核例程窗口驱动程序工具包 (WDK) 标头文件中定义的许多有用的宏。 这些宏的一些通常情况下使用而不是直接调用 RDBSS 例程。 一些这些宏用作方便例程。

由 RDBSS 定义以下宏。

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
<td align="left"><p><strong>RxAcquirePrefixTableLockExclusive</strong> (<em>TABLE</em>, <em>WAIT</em>)</p></td>
<td align="left"><p>此宏获取独占模式下更改操作为该前缀表锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxAcquirePrefixTableLockShared</strong> (<em>表</em>，<em>等待</em>)</p></td>
<td align="left"><p>此宏获取前缀表锁在共享模式下的查找操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxAllocatePoolWithTag</strong> (<em>type</em>, <em>size</em>, <em>tag</em>)</p></td>
<td align="left"><p>在 checked 版本中，此宏从具有四个字节标记可用于帮助捕获实例的内存移入垃圾桶块的开始处的池分配内存。</p>
<p>在零售版本中，此宏将成为直接调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544520" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544520)"> <strong>ExAllocatePoolWithTag</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxCheckMemoryBlock</strong> (<em>ptr</em>)</p></td>
<td align="left"><p>在 checked 版本中，此宏会检查特殊的 RX_POOL_HEADER 标头签名的内存块。</p>
<p>在零售版本，此宏没有任何影响。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceAndFinalizeNetFcb</strong> (<em>Fcb ,RxContext</em>, <em>RecursiveFinalize</em>, <em>ForceFinalize</em>)</p></td>
<td align="left"><p>使用此宏来跟踪取消引用 FCB 结构上的操作。</p>
<p>请注意，此宏操作的引用计数也会返回最终的取消引用调用的状态。</p></td>
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
<td align="left"><p>使用此宏来跟踪取消引用 V_NET_ROOT 结构上的操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxFcbAcquiredShared</strong> (<em>RXCONTEXT</em>, <em>FCB</em>)</p></td>
<td align="left"><p>此宏检查当前线程是否在共享模式下具有常规资源的访问权限。 此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545477" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545477)"> <strong>ExIsResourceAcquiredSharedLite</strong> </a>例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxFillAndInstallFastIoDispatch</strong>(<em>__devobj</em>, <em>__fastiodisp</em>)</p></td>
<td align="left"><p>此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff557374" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557374)"> <strong>__RxFillAndInstallFastIoDispatch</strong> </a>填写快速 I/O 调度向量相同正常调度 I/O 向量，其驱动程序对象与关联的安装传递的设备对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxFreePool</strong> (<em>ptr</em>)</p></td>
<td align="left"><p>在 checked 版本中，此宏可释放的内存池。</p>
<p>在零售版本中，此宏将成为直接调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544590" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544590)"> <strong>ExFreePool</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsFcbAcquiredShared</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>此宏检查当前线程是否在共享模式下具有常规资源的访问权限。 此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545477" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545477)"> <strong>ExIsResourceAcquiredSharedLite</strong> </a>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsFcbAcquiredExclusive</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>此宏检查当前线程具有独占模式下对常规资源的访问。 此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545458" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545458)"> <strong>ExIsResourceAcquiredExclusiveLite</strong> </a>例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsFcbAcquired</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>此宏检查当前线程是否在共享或排他模式下具有常规资源的访问权限。 此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545477" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545477)"> <strong>ExIsResourceAcquiredSharedLite</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff545458" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545458)"> <strong>ExIsResourceAcquiredExclusiveLite</strong> </a>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsPrefixTableLockAcquired</strong> (<em>TABLE</em>)</p></td>
<td align="left"><p>此宏指示是否在独占或共享模式下获取前缀表锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsPrefixTableLockExclusive</strong> (<em>TABLE</em>)</p></td>
<td align="left"><p>此宏指示是否以独占方式获取前缀表锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLog</strong>(<em>Args</em>)</p></td>
<td align="left"><p>此宏调用检查内部版本号<a href="https://msdn.microsoft.com/library/windows/hardware/ff557368" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557368)"> <strong>_RxLog</strong> </a>例程。</p>
<p>在零售版本，此宏没有任何影响。</p>
<p>请注意，参数<strong>RxLog</strong>必须为括在一对括号，若要启用翻译为 null 的调用时应关闭日志记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogEvent</strong> (<em>_DeviceObject</em>, <em>_OriginatorId</em>, <em>_EventId</em>, <em>_Status</em>)</p></td>
<td align="left"><p>此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff554515" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554515)"> <strong>RxLogEventDirect</strong> </a>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogFailure</strong> (<em>_DeviceObject</em>, <em>_OriginatorId</em>, <em>_EventId</em>, <em>_Status</em>)</p></td>
<td align="left"><p>此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff554515" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554515)"> <strong>RxLogEventDirect</strong> </a>例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogFailureWithBuffer</strong> (<em>_DeviceObject</em>, <em>_OriginatorId</em>, <em>_EventId</em>, <em>_Status</em>, <em>_Buffer</em>, <em>_Length</em>)</p></td>
<td align="left"><p>此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff554524" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554524)"> <strong>RxLogEventWithBufferDirect</strong> </a>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogRetail</strong>(<em>Args</em>)</p></td>
<td align="left"><p>此宏调用检查内部版本号<a href="https://msdn.microsoft.com/library/windows/hardware/ff557368" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557368)"> <strong>_RxLog</strong> </a>例程。</p>
<p>在零售版本，此宏没有任何影响。</p>
<p>请注意，参数<strong>RxLogRetail</strong>必须为括在一对括号，若要启用翻译为 null 的调用时应关闭日志记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceNetFcb</strong> (<em>Fcb</em>)</p></td>
<td align="left"><p>此宏用于跟踪对 FCB 结构的引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceNetFobx</strong> (<em>Fobx</em>)</p></td>
<td align="left"><p>此宏用于跟踪对 FOBX 结构的引用操作。 可以通过日志记录系统和 WMI 访问这些引用操作的日志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceNetRoot</strong> (<em>NetRoot</em>)</p></td>
<td align="left"><p>此宏用于跟踪对 NET_ROOT 结构的引用操作。 可以通过日志记录系统和 Windows Management Instrumentation (WMI) 访问这些引用操作的日志。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceSrvCall</strong> (<em>SrvCall</em>)</p></td>
<td align="left"><p>此宏用于跟踪对 SRV_CALL 结构不在延迟过程调用 (DPC) 级别的引用操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceSrvCallAtDpc</strong> (<em>SrvCall</em>)</p></td>
<td align="left"><p>此宏用于跟踪对在 DPC 级别 SRV_CALL 结构的引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceSrvOpen</strong> (<em>SrvOpen</em>)</p></td>
<td align="left"><p>此宏用于跟踪对 SRV_OPEN 结构的引用操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceVNetRoot</strong> (<em>VNetRoot</em>)</p></td>
<td align="left"><p>此宏用于跟踪对 V_NET_ROOT 结构的引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReleasePrefixTableLock</strong> (<em>TABLE</em>)</p></td>
<td align="left"><p>此宏可释放前缀表锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong>(<em>RXCONTEXT</em>,<em>FCB</em>,<em>IOQUEUE</em>)</p></td>
<td align="left"><p>此宏会同步到相同的工作队列的阻塞 I/O 请求。 在 Windows Server 2003 上此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff557377" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperations&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557377)"> <strong>__RxSynchronizeBlockingOperations</strong> </a>例程替换<em>DropFcbLock</em>参数设置为<strong>FALSE</strong>.</p>
<p>在 Windows XP 和 Windows 2000 上，此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff557382" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557382)"> <strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong> </a>例程替换<em>DropFcbLock</em>参数设置为<strong>FALSE</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong>(<em>RXCONTEXT</em>,<em>FCB</em>,<em>IOQUEUE</em>)</p></td>
<td align="left"><p>此宏会同步到相同的工作队列的阻塞 I/O 请求。 在 Windows Server 2003 上此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff557377" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperations&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557377)"> <strong>__RxSynchronizeBlockingOperations</strong> </a>例程替换<em>DropFcbLock</em>参数设置为<strong>TRUE</strong>.</p>
<p>在 Windows XP 和 Windows 2000 上，此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff557382" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557382)"> <strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong> </a>例程替换<em>DropFcbLock</em>参数设置为<strong>，则返回 TRUE</strong>。</p></td>
</tr>
</tbody>
</table>

 

 

 




