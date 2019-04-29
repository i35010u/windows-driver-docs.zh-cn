---
title: 修改可发出 I/O 请求的代码
description: 修改可发出 I/O 请求的代码
ms.assetid: 39E4B6B2-45C8-42B7-811A-EEDCCCB056EF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bcfaa8cc3ecf1303223c3f80df81fd2d94f7e0d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325172"
---
# <a name="revise-code-that-issues-io-requests"></a>修改可发出 I/O 请求的代码


WDF 定义多个驱动程序可用于创建和格式化 I/O 请求的方法。 下表总结了这些方法：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">KMDF 方法</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548604" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForIoctl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548604)"><strong>WdfIoTargetFormatRequestForIoctl</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548595" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548595)"><strong>WdfIoTargetFormatRequestForInternalIoctl</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548599" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctlOthers&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548599)"><strong>WdfIoTargetFormatRequestForInternalIoctlOthers</strong></a></p></td>
<td align="left">类似于手动设置格式的下一步的 I/O 堆栈位置。</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548612" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForRead&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548612)"><strong>WdfIoTargetFormatRequestForRead</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548620" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForWrite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548620)"><strong>WdfIoTargetFormatRequestForWrite</strong></a></p></td>
<td align="left">类似于<a href="https://msdn.microsoft.com/library/windows/hardware/ff548310" data-raw-source="[&lt;strong&gt;IoBuildAsynchronousFsdRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548310)"> <strong>IoBuildAsynchronousFsdRequest</strong></a>。</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548660" data-raw-source="[&lt;strong&gt;WdfIoTargetSendIoctlSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548660)"><strong>WdfIoTargetSendIoctlSynchronously</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548656" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548656)"><strong>WdfIoTargetSendInternalIoctlSynchronously</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548651" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlOthersSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548651)"><strong>WdfIoTargetSendInternalIoctlOthersSynchronously</strong></a></p></td>
<td align="left">类似于<a href="https://msdn.microsoft.com/library/windows/hardware/ff548318" data-raw-source="[&lt;strong&gt;IoBuildDeviceIoControlRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548318)"> <strong>IoBuildDeviceIoControlRequest</strong></a>后, 跟<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"> <strong>IoCallDriver</strong></a>。</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548669" data-raw-source="[&lt;strong&gt;WdfIoTargetSendReadSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548669)"><strong>WdfIoTargetSendReadSynchronously</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548672" data-raw-source="[&lt;strong&gt;WdfIoTargetSendWriteSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548672)"><strong>WdfIoTargetSendWriteSynchronously</strong></a></p></td>
<td align="left">类似于<a href="https://msdn.microsoft.com/library/windows/hardware/ff548330" data-raw-source="[&lt;strong&gt;IoBuildSynchronousFsdRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548330)"> <strong>IoBuildSynchronousFsdRequest</strong></a>后, 跟<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"> <strong>IoCallDriver</strong></a>。</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549941" data-raw-source="[&lt;strong&gt;WdfRequestCancelSentRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549941)"><strong>WdfRequestCancelSentRequest</strong></a></p></td>
<td align="left">类似于<a href="https://msdn.microsoft.com/library/windows/hardware/ff548338" data-raw-source="[&lt;strong&gt;IoCancelIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548338)"> <strong>IoCancelIrp</strong> </a>的已发送 PIRP <a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"> <strong>IoCallDriver</strong></a>。 该框架提供了锁，以确保未完成或释放对的调用之间 PIRP <strong>IoCallDriver</strong>并<strong>IoCancelIrp</strong>。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549951" data-raw-source="[&lt;strong&gt;WdfRequestCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549951)"><strong>WdfRequestCreate</strong></a></td>
<td align="left">类似于<a href="https://msdn.microsoft.com/library/windows/hardware/ff548257" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548257)"> <strong>IoAllocateIrp</strong></a>。 创建一个新的 WDFREQUEST 对象、 设置属性，并返回到调用方的句柄。</td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff549955" data-raw-source="[&lt;strong&gt;WdfRequestFormatRequestUsingCurrentType&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549955)"><strong>WdfRequestFormatRequestUsingCurrentType</strong></a></td>
<td align="left">类似于<a href="https://msdn.microsoft.com/library/windows/hardware/ff549100" data-raw-source="[&lt;strong&gt;IoForwardIrpSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549100)"> <strong>IoForwardIrpSynchronously</strong> </a>但不会调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"> <strong>IoCallDriver</strong></a>; 驱动程序必须调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff550027" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550027)"> <strong>WdfRequestSend</strong></a>。</td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff550027" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550027)"><strong>WdfRequestSend</strong></a></td>
<td align="left">类似于<a href="https://msdn.microsoft.com/library/windows/hardware/ff549100" data-raw-source="[&lt;strong&gt;IoForwardIrpSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549100)"> <strong>IoForwardIrpSynchronously</strong> </a>但不会调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548336" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548336)"> <strong>IoCallDriver</strong></a>; 驱动程序必须调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff550027" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550027)"> <strong>WdfRequestSend</strong></a>。</td>
</tr>
</tbody>
</table>

 

若要将请求发送到另一个设备堆栈，WDF 驱动程序将使用远程 I/O 目标。 有关如何初始化远程 I/O 目标的信息，请参阅[初始化常规 I/O 目标](initializing-a-general-i-o-target.md)。

若要获取的完成状态的异步请求或通过调用发送任何请求[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)，驱动程序调用[ **WdfRequestGetStatus**](https://msdn.microsoft.com/library/windows/hardware/ff549974). 对于同步请求，它可以立即检索状态。 对于异步请求，驱动程序的 I/O 完成回调通常检索状态。 有关同步或异步发送请求的详细信息，请参阅[将 I/O 请求发送到常规 I/O 目标](sending-i-o-requests-to-general-i-o-targets.md)。

 

 





