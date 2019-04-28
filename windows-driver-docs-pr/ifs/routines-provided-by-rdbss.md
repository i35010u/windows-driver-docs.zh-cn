---
title: RDBSS 提供的例程
description: RDBSS 提供的例程
ms.assetid: 37631760-ac89-4ef0-ad7c-ed3e68aa1ceb
keywords:
- RDBSS WDK 的文件系统例程
- 重定向驱动器缓冲子系统 WDK 的文件系统例程
- 例程 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e9cf8ad4fca1e49587e59ea7e836da972975c47
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344531"
---
# <a name="routines-provided-by-rdbss"></a>RDBSS 提供的例程


## <span id="ddk_functions_provided_by_rdbss_if"></span><span id="DDK_FUNCTIONS_PROVIDED_BY_RDBSS_IF"></span>


下面的例程都由 RDBSS 导出。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553363" data-raw-source="[&lt;strong&gt;RxAcquireExclusiveFcbResourceInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553363)"><strong>RxAcquireExclusiveFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>此资源获取例程获取排他模式中的文件控制块 (FCB) 资源。 此例程将等待 FCB 资源是免费的因此此例程不返回控件之前获取资源。 此例程获取 FCB 资源，即使已取消与此 FCB RX_CONTEXT。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553372" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553372)"><strong>RxAcquireSharedFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>此资源获取例程将获取在共享模式下的 FCB 资源。 此例程将等待 FCB 资源是如果以前以独占方式，获取免费的因此此例程不返回控件之前获取资源。 此例程获取 FCB 资源，即使已取消与此 FCB RX_CONTEXT。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff553375" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553375)"><strong>RxAcquireSharedFcbResourceInMRxEx</strong></a></td>
<td align="left"><p>此资源获取例程将获取在共享模式下的 FCB 资源。 此例程将等待 FCB 资源，如果以前以独占方式获取要释放。 此例程不返回控件，直到获取资源。 此例程获取 FCB 资源，即使已取消与此 FCB RX_CONTEXT。</p>
<p>Windows Server 2003 Service Pack 1 (SP1) 及更高版本，此例程才可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553384" data-raw-source="[&lt;strong&gt;RxAssert&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553384)"><strong>RxAssert</strong></a></p></td>
<td align="left"><p>此例程将发送 RDBSS 检查中的 assert 字符串到内核调试程序安装一个的情况下生成。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553388" data-raw-source="[&lt;strong&gt;RxAssociateContextWithMid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553388)"><strong>RxAssociateContextWithMid</strong></a></p></td>
<td align="left"><p>此例程将提供的不透明上下文相关联的可用 multiplex ID (MID) 从 MID_ATLAS 数据结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553395" data-raw-source="[&lt;strong&gt;RxCancelTimerRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553395)"><strong>RxCancelTimerRequest</strong></a></p></td>
<td align="left"><p>此例程会取消计时器请求。 若要取消该请求由例程和上下文标识。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553405" data-raw-source="[&lt;strong&gt;RxCeAllocateIrpWithMDL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553405)"><strong>RxCeAllocateIrpWithMDL</strong></a></p></td>
<td align="left"><p>此例程由连接引擎用于分配 IRP，并将 MDL 与 IRP 相关联。</p>
<p>此例程才可在 Windows XP 上。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553414" data-raw-source="[&lt;strong&gt;RxCeBuildAddress&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553414)"><strong>RxCeBuildAddress</strong></a></p></td>
<td align="left"><p>此例程将与传输绑定关联的传输地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553417" data-raw-source="[&lt;strong&gt;RxCeBuildConnection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553417)"><strong>RxCeBuildConnection</strong></a></p></td>
<td align="left"><p>此例程建立本地 RDBSS 连接地址与给定的远程地址之间的连接。 此例程应调用的系统工作线程上下文中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553424" data-raw-source="[&lt;strong&gt;RxCeBuildConnectionOverMultipleTransports&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553424)"><strong>RxCeBuildConnectionOverMultipleTransports</strong></a></p></td>
<td align="left"><p>此例程建立本地 RDBSS 连接地址和给定的远程地址之间的连接，并支持多个传输协议。 指定一组的本地地址，此例程会尝试连接到使用本地地址与关联的传输的所有目标服务器。 作为入选方，具体取决于连接选项选择一个连接。 必须在系统工作线程的上下文中调用此例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553434" data-raw-source="[&lt;strong&gt;RxCeBuildTransport&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553434)"><strong>RxCeBuildTransport</strong></a></p></td>
<td align="left"><p>此例程将 RDBSS 传输绑定到指定的传输名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553439" data-raw-source="[&lt;strong&gt;RxCeBuildVC&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553439)"><strong>RxCeBuildVC</strong></a></p></td>
<td align="left"><p>此例程将虚拟线路添加到指定的连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553440" data-raw-source="[&lt;strong&gt;RxCeCancelConnectRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553440)"><strong>RxCeCancelConnectRequest</strong></a></p></td>
<td align="left"><p>此例程将取消以前颁发的连接请求。</p>
<p>请注意，当前未实现此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553448" data-raw-source="[&lt;strong&gt;RxCeFreeIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553448)"><strong>RxCeFreeIrp</strong></a></p></td>
<td align="left"><p>此例程将释放 IRP 引擎使用的连接。</p>
<p>此例程才可在 Windows XP 上。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553454" data-raw-source="[&lt;strong&gt;RxCeInitiateVCDisconnect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553454)"><strong>RxCeInitiateVCDisconnect</strong></a></p></td>
<td align="left"><p>此例程启动虚拟线路上的断开连接。 必须在系统工作线程的上下文中调用此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553456" data-raw-source="[&lt;strong&gt;RxCeQueryAdapterStatus&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553456)"><strong>RxCeQueryAdapterStatus</strong></a></p></td>
<td align="left"><p>此例程将返回给定传输 ADAPTER_STATUS 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553461" data-raw-source="[&lt;strong&gt;RxCeQueryInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553461)"><strong>RxCeQueryInformation</strong></a></p></td>
<td align="left"><p>此例程查询有关给定虚拟线路的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553474" data-raw-source="[&lt;strong&gt;RxCeQueryTransportInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553474)"><strong>RxCeQueryTransportInformation</strong></a></p></td>
<td align="left"><p>此例程将查询给定的传输的连接数和服务的质量有关的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553479" data-raw-source="[&lt;strong&gt;RxCeSend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553479)"><strong>RxCeSend</strong></a></p></td>
<td align="left"><p>此例程将传输服务的数据单元 (TSDU) 发送沿虚拟线路上指定的连接。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553482" data-raw-source="[&lt;strong&gt;RxCeSendDatagram&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553482)"><strong>RxCeSendDatagram</strong></a></p></td>
<td align="left"><p>此例程将 TSDU 发送到指定的传输地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553488" data-raw-source="[&lt;strong&gt;RxCeTearDownAddress&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553488)"><strong>RxCeTearDownAddress</strong></a></p></td>
<td align="left"><p>此例程中删除从传输绑定的传输地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554321" data-raw-source="[&lt;strong&gt;RxCeTearDownConnection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554321)"><strong>RxCeTearDownConnection</strong></a></p></td>
<td align="left"><p>此例程解除对给定的实例。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554328" data-raw-source="[&lt;strong&gt;RxCeTearDownTransport&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554328)"><strong>RxCeTearDownTransport</strong></a></p></td>
<td align="left"><p>此例程解除绑定从指定的传输。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554332" data-raw-source="[&lt;strong&gt;RxCeTearDownVC&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554332)"><strong>RxCeTearDownVC</strong></a></p></td>
<td align="left"><p>此例程卸除的虚拟连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554335" data-raw-source="[&lt;strong&gt;RxChangeBufferingState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554335)"><strong>RxChangeBufferingState</strong></a></p></td>
<td align="left"><p>此例程调用以处理缓冲的状态更改请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554340" data-raw-source="[&lt;strong&gt;RxCompleteRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554340)"><strong>RxCompleteRequest</strong></a></p></td>
<td align="left"><p>此例程用于完成 IRP 与 RX_CONTEXT 结构相关联。 此例程 RDBSS 供内部使用和不能由网络微型重定向程序驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554348" data-raw-source="[&lt;strong&gt;RxCompleteRequest_Real&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554348)"><strong>RxCompleteRequest_Real</strong></a></p></td>
<td align="left"><p>此例程用于完成 IRP 与 RX_CONTEXT 结构相关联。 此例程不应通过网络微型-重定向程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554352" data-raw-source="[&lt;strong&gt;RxCreateMidAtlas&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554352)"><strong>RxCreateMidAtlas</strong></a></p></td>
<td align="left"><p>此例程分配 MID_ATLAS 数据结构的新实例并初始化它。 RDBSS 使用 multiplex ID (MID) 在这种数据结构中定义为网络客户端 （最小-重定向程序） 和服务器可区分对任何连接的并发活动请求的方式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554356" data-raw-source="[&lt;strong&gt;RxCreateNetFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554356)"><strong>RxCreateNetFcb</strong></a></p></td>
<td align="left"><p>此例程分配、 初始化，并将新的 FCB 结构插入到其打开此 FCB 的 NET_ROOT 结构的内存中数据结构。 分配的结构 SRV_OPEN 和 FOBX 结构有空间。 此例程 RDBSS 供内部使用和不能由网络微型重定向程序驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554358" data-raw-source="[&lt;strong&gt;RxCreateNetFobx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554358)"><strong>RxCreateNetFobx</strong></a></p></td>
<td align="left"><p>此例程分配、 初始化，并将插入新的文件对象扩展 (FOBX) 结构。 网络微型-重定向程序应调用此例程的末尾创建 FOBX 成功创建操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554366" data-raw-source="[&lt;strong&gt;RxCreateNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554366)"><strong>RxCreateNetRoot</strong></a></p></td>
<td align="left"><p>此例程生成表示 NET_ROOT 结构的节点，并将名称插入到关联的设备对象上的网络名称表。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554367" data-raw-source="[&lt;strong&gt;RxCreateRxContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554367)"><strong>RxCreateRxContext</strong></a></p></td>
<td align="left"><p>此例程分配新的 RX_CONTEXT 结构并初始化数据结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554370" data-raw-source="[&lt;strong&gt;RxCreateSrvCall&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554370)"><strong>RxCreateSrvCall</strong></a></p></td>
<td align="left"><p>此例程生成一个表示服务器调用上下文并将其插入到 RDBSS 维护的网络名表名称的节点。 此例程 RDBSS 供内部使用和不能由网络微型重定向程序驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554376" data-raw-source="[&lt;strong&gt;RxCreateSrvOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554376)"><strong>RxCreateSrvOpen</strong></a></p></td>
<td align="left"><p>此例程分配、 初始化，并将新的 SRV_OPEN 结构插入到 RDBSS 所使用的内存中数据结构。 如果要分配新的结构，它具有为 FOBX 结构的空间。 此例程 RDBSS 供内部使用和不能由网络微型重定向程序驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554380" data-raw-source="[&lt;strong&gt;RxCreateVNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554380)"><strong>RxCreateVNetRoot</strong></a></p></td>
<td align="left"><p>此例程生成表示 V_NET_ROOT 结构和网络名称表中插入名称的节点。 此例程 RDBSS 供内部使用和不能由网络微型重定向程序驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554385" data-raw-source="[&lt;strong&gt;RxDbgBreakPoint&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554385)"><strong>RxDbgBreakPoint</strong></a></p></td>
<td align="left"><p>此例程会引发异常，如果已安装; 由内核调试程序否则，它是由调试系统进行处理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554388" data-raw-source="[&lt;strong&gt;RxDereference&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554388)"><strong>RxDereference</strong></a></p></td>
<td align="left"><p>此例程递减引用计数在多个引用计数的数据结构的实例由 RDBSS。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554393" data-raw-source="[&lt;strong&gt;RxDereferenceAndDeleteRxContext_Real&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554393)"><strong>RxDereferenceAndDeleteRxContext_Real</strong></a></p></td>
<td align="left"><p>此例程取消引用 RX_CONTEXT 结构和如果引用计数变为零，然后它会解除分配并将删除指定的 RX_CONTEXT 结构从 RDBSS 内存中数据结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554395" data-raw-source="[&lt;strong&gt;RxDestroyMidAtlas&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554395)"><strong>RxDestroyMidAtlas</strong></a></p></td>
<td align="left"><p>此例程销毁 MID_ATLAS 数据结构的现有实例，并释放分配的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554398" data-raw-source="[&lt;strong&gt;RxDispatchToWorkerThread&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554398)"><strong>RxDispatchToWorkerThread</strong></a></p></td>
<td align="left"><p>此例程调用的工作线程的上下文中的例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554404" data-raw-source="[&lt;strong&gt;RxDriverEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554404)"><strong>RxDriverEntry</strong></a></p></td>
<td align="left"><p>此例程称为由单一式网络微型重定向程序驱动程序从其<strong>DriverEntry</strong>初始化 RDBSS。</p>
<p>对于非整体化驱动程序，此初始化例程等同于<strong>DriverEntry</strong>的日常<em>rdbss.sys</em>设备驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554409" data-raw-source="[&lt;strong&gt;RxFinalizeConnection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554409)"><strong>RxFinalizeConnection</strong></a></p></td>
<td align="left"><p>此例程会删除到共享的连接。 根据指定的强制级别关闭的连接上打开任何文件。 网络微型重定向可能选择使传输连接保持打开状态出于性能原因，除非指定的选项以强制关闭连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554412" data-raw-source="[&lt;strong&gt;RxFinalizeNetFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554412)"><strong>RxFinalizeNetFcb</strong></a></p></td>
<td align="left"><p>此例程完成给定的 FCB 结构。 调用方必须具有与 FCB 相关联的 NET_ROOT 结构的排他锁。 此例程 RDBSS 供内部使用和不能由网络微型重定向程序驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554418" data-raw-source="[&lt;strong&gt;RxFinalizeNetFobx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554418)"><strong>RxFinalizeNetFobx</strong></a></p></td>
<td align="left"><p>此例程完成给定的 FOBX 结构。 调用方必须具有与此 FOBX 相关联的 FCB 的排他锁。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554421" data-raw-source="[&lt;strong&gt;RxFinalizeNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554421)"><strong>RxFinalizeNetRoot</strong></a></p></td>
<td align="left"><p>此例程完成给定的 NET_ROOT 结构。 调用方应与此 NET_ROOT 结构 （通过 SRV_CALL 结构） 关联的设备对象对 NetName 表具有对锁的独占访问权限。 此例程 RDBSS 供内部使用和不能由网络微型重定向程序驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554426" data-raw-source="[&lt;strong&gt;RxFinalizeSrvCall&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554426)"><strong>RxFinalizeSrvCall</strong></a></p></td>
<td align="left"><p>此例程完成给定的 SRV_CALL 结构。 调用方应与此 SRV_CALL 结构关联的设备对象对 NetName 表具有对锁的独占访问权限。 此例程 RDBSS 供内部使用和不能由网络微型重定向程序驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554432" data-raw-source="[&lt;strong&gt;RxFinalizeSrvOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554432)"><strong>RxFinalizeSrvOpen</strong></a></p></td>
<td align="left"><p>此例程完成给定的 SRV_OPEN 结构。 此例程 RDBSS 供内部使用和不能由网络微型重定向程序驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554450" data-raw-source="[&lt;strong&gt;RxFinalizeVNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554450)"><strong>RxFinalizeVNetRoot</strong></a></p></td>
<td align="left"><p>此例程完成给定的 V_NET_ROOT 结构。 调用方必须具有与此 V_NET_ROOT 结构关联的设备对象的 NetName 表锁的独占访问权限。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554454" data-raw-source="[&lt;strong&gt;RxFinishFcbInitialization&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554454)"><strong>RxFinishFcbInitialization</strong></a></p></td>
<td align="left"><p>此例程用于通过网络微型重定向完成的创建操作成功完成后初始化 FCB。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554463" data-raw-source="[&lt;strong&gt;RxForceFinalizeAllVNetRoots&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554463)"><strong>RxForceFinalizeAllVNetRoots</strong></a></p></td>
<td align="left"><p>此例程强制完成所有与给定 NET_ROOT 结构相关联的 V_NET_ROOT 结构。 调用方必须具有与此 V_NET_ROOT 结构关联的设备对象的 NetName 表锁的独占访问权限。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554468" data-raw-source="[&lt;strong&gt;RxFsdDispatch&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554468)"><strong>RxFsdDispatch</strong></a></p></td>
<td align="left"><p>此例程实现 RDBSS 来处理 I/O 请求数据包 (IRP) 文件系统驱动程序 (FSD) 调度。 此例程称为通过网络微型-重定向程序驱动程序调度例程启动 RDBSS 处理的请求中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554472" data-raw-source="[&lt;strong&gt;RxFsdPostRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554472)"><strong>RxFsdPostRequest</strong></a></p></td>
<td align="left"><p>此例程排队 I/O 请求数据包 (IRP) 到辅助队列中等待处理的 RX_CONTEXT 结构由文件系统进程 (FSP)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554478" data-raw-source="[&lt;strong&gt;RxGetFileSizeWithLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554478)"><strong>RxGetFileSizeWithLock</strong></a></p></td>
<td align="left"><p>此例程使用锁来确保一致读取的 64 位值的 FCB 结构中获取文件大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554481" data-raw-source="[&lt;strong&gt;RxGetRDBSSProcess&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554481)"><strong>RxGetRDBSSProcess</strong></a></p></td>
<td align="left"><p>此例程返回一个指向 RDBSS 内核进程使用的主线程的过程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554485" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554485)"><strong>RxIndicateChangeOfBufferingState</strong></a></p></td>
<td align="left"><p>此例程称为注册以供将来处理缓冲状态更改请求 （oplock 中断指示）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554490" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingStateForSrvOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554490)"><strong>RxIndicateChangeOfBufferingStateForSrvOpen</strong></a></p></td>
<td align="left"><p>此例程称为注册以供将来处理缓冲状态更改请求 （oplock 中断指示）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554493" data-raw-source="[&lt;strong&gt;RxInferFileType&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554493)"><strong>RxInferFileType</strong></a></p></td>
<td align="left"><p>此例程会尝试推断 （目录或非目录） 的文件类型从<strong>CreateOptions</strong> ( <strong>Create.NtCreateParameters.CreateOptions</strong>) 字段中 RX_CONTEXT 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554502" data-raw-source="[&lt;strong&gt;RxInitializeContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554502)"><strong>RxInitializeContext</strong></a></p></td>
<td align="left"><p>此例程初始化新分配的 RX_CONTEXT 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554508" data-raw-source="[&lt;strong&gt;RxIsThisACscAgentOpen&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554508)"><strong>RxIsThisACscAgentOpen</strong></a></p></td>
<td align="left"><p>此例程确定打开的文件可能由用户模式下客户端的缓存代理。</p>
<p>此例程才可在 Windows Server 2003 上。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554511" data-raw-source="[&lt;strong&gt;RxLockEnumerator&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554511)"><strong>RxLockEnumerator</strong></a></p></td>
<td align="left"><p>此例程称为从网络微型重定向来枚举 FCB 的文件锁定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554515" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554515)"><strong>RxLogEventDirect</strong></a></p></td>
<td align="left"><p>此例程称为到 I/O 错误日志记录的错误。 建议<strong>RxLogEvent</strong>或<strong>RxLogFailure</strong>而不是直接调用该例程使用宏。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554519" data-raw-source="[&lt;strong&gt;RxLogEventWithAnnotation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554519)"><strong>RxLogEventWithAnnotation</strong></a></p></td>
<td align="left"><p>此例程分配的 I/O 错误日志结构、 填充在该日志结构，并将此结构写入到 I/O 错误日志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554524" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554524)"><strong>RxLogEventWithBufferDirect</strong></a></p></td>
<td align="left"><p>此例程称为到 I/O 错误日志记录的错误。 此例程编码为存储在 I/O 错误日志结构的数据缓冲区的行号和状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554525" data-raw-source="[&lt;strong&gt;RxLowIoCompletion&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554525)"><strong>RxLowIoCompletion</strong></a></p></td>
<td align="left"><p>此例程必须调用由网络微型重定向程序驱动程序的较低的 I/O 例程处理完成后，如果该例程返回最初挂起。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554529" data-raw-source="[&lt;strong&gt;RxLowIoGetBufferAddress&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554529)"><strong>RxLowIoGetBufferAddress</strong></a></p></td>
<td align="left"><p>此例程返回对应的缓冲区到从 MDL <strong>LowIoContext</strong> RX_CONTEXT 结构的结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554532" data-raw-source="[&lt;strong&gt;RxMakeLateDeviceAvailable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554532)"><strong>RxMakeLateDeviceAvailable</strong></a></p></td>
<td align="left"><p>此例程修改设备对象，从而使"后期设备"可用。 后期设备是指不在驱动程序的负载例程中创建。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554541" data-raw-source="[&lt;strong&gt;RxMapAndDissociateMidFromContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554541)"><strong>RxMapAndDissociateMidFromContext</strong></a></p></td>
<td align="left"><p>此例程将 MID 映射到 MID_ATLAS 数据结构中其关联的上下文，并取消从上下文 MID 然后关联。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554545" data-raw-source="[&lt;strong&gt;RxMapMidToContext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554545)"><strong>RxMapMidToContext</strong></a></p></td>
<td align="left"><p>此例程会映射到 MID_ATLAS 数据结构中其关联的上下文 MID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554549" data-raw-source="[&lt;strong&gt;RxMapSystemBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554549)"><strong>RxMapSystemBuffer</strong></a></p></td>
<td align="left"><p>此例程返回 I/O 请求数据包 (IRP) 从系统缓冲区地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554552" data-raw-source="[&lt;strong&gt;RxNameCacheActivateEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554552)"><strong>RxNameCacheActivateEntry</strong></a></p></td>
<td align="left"><p>此例程采用名称缓存项，并更新的到期时间和网络微型重定向程序上下文。 然后将该条目放在活动的列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554558" data-raw-source="[&lt;strong&gt;RxNameCacheCheckEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554558)"><strong>RxNameCacheCheckEntry</strong></a></p></td>
<td align="left"><p>此例程将检查有效性的 NAME_CACHE 条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554565" data-raw-source="[&lt;strong&gt;RxNameCacheCreateEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554565)"><strong>RxNameCacheCreateEntry</strong></a></p></td>
<td align="left"><p>此例程分配并初始化具有给定名称字符串的 NAME_CACHE 结构。 应调用方将然后初始化的任何其他网络微型重定向程序元素的名称缓存上下文，然后将条目放在名称缓存活动列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554569" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554569)"><strong>RxNameCacheExpireEntry</strong></a></p></td>
<td align="left"><p>此例程将 NAME_CACHE 条目置于空闲列表上。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554570" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntryWithShortName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554570)"><strong>RxNameCacheExpireEntryWithShortName</strong></a></p></td>
<td align="left"><p>此例程将过期的所有 NAME_CACHE 条目其名称前缀匹配给定的短文件名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554573" data-raw-source="[&lt;strong&gt;RxNameCacheFetchEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554573)"><strong>RxNameCacheFetchEntry</strong></a></p></td>
<td align="left"><p>此例程中查找匹配项替换为 NAME_CACHE 条目指定的名称字符串。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554575" data-raw-source="[&lt;strong&gt;RxNameCacheFinalize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554575)"><strong>RxNameCacheFinalize</strong></a></p></td>
<td align="left"><p>此例程将释放所有 NAME_CACHE 条目与 NAME_CACHE_CONTROL 结构相关联的存储。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554579" data-raw-source="[&lt;strong&gt;RxNameCacheFreeEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554579)"><strong>RxNameCacheFreeEntry</strong></a></p></td>
<td align="left"><p>此例程释放 NAME_CACHE 项存储并递减的 NAME_CACHE 计数缓存条目与 NAME_CACHE_CONTROL 结构相关联。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554586" data-raw-source="[&lt;strong&gt;RxNameCacheInitialize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554586)"><strong>RxNameCacheInitialize</strong></a></p></td>
<td align="left"><p>此例程初始化 NAME_CACHE 结构，并将其与 NAME_CACHE_CONTROL 结构关联。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554591" data-raw-source="[&lt;strong&gt;RxNewMapUserBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554591)"><strong>RxNewMapUserBuffer</strong></a></p></td>
<td align="left"><p>此例程将返回为低 I/O 所使用的用户缓冲区的地址。</p>
<p>此例程才在 Windows XP 和 Windows 2000 上可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554595" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockExclusive&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554595)"><strong>RxpAcquirePrefixTableLockExclusive</strong></a></p></td>
<td align="left"><p>此例程将获取对目录 SRV_CALL 和 NET_ROOT 名称所用的前缀表的排他锁。</p>
<p>此例程才在 Windows XP 和 Windows 2000 上可用。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554598" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockShared&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554598)"><strong>RxpAcquirePrefixTableLockShared</strong></a></p></td>
<td align="left"><p>此例程将获取对目录 SRV_CALL 和 NET_ROOT 名称所用的前缀表上的共享的锁。</p>
<p>此例程才在 Windows XP 和 Windows 2000 上可用。 此例程 RDBSS 供内部使用和不能由网络微型重定向程序驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff554603" data-raw-source="[&lt;strong&gt;RxpDereferenceAndFinalizeNetFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554603)"><strong>RxpDereferenceAndFinalizeNetFcb</strong></a></td>
<td align="left"><p>此例程临近 FCB 以及取消引用的引用计数。</p>
<p>Windows Server 2003 Service Pack 1 (SP1) 及更高版本，此例程才可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554608" data-raw-source="[&lt;strong&gt;RxpDereferenceNetFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554608)"><strong>RxpDereferenceNetFcb</strong></a></p></td>
<td align="left"><p>此例程递减 FCB 的引用计数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554612" data-raw-source="[&lt;strong&gt;RxPostOneShotTimerRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554612)"><strong>RxPostOneShotTimerRequest</strong></a></p></td>
<td align="left"><p>驱动程序使用此例程来初始化一次性计时器请求。 传递给此例程的辅助角色线程例程后计时器过期时调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554615" data-raw-source="[&lt;strong&gt;RxPostRecurrentTimerRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554615)"><strong>RxPostRecurrentTimerRequest</strong></a></p></td>
<td align="left"><p>此例程用于初始化循环计时器请求。 辅助角色线程例程，传递给此例程称为按固定间隔重复的计时器将激发时基于此例程的输入参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554620" data-raw-source="[&lt;strong&gt;RxPostToWorkerThread&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554620)"><strong>RxPostToWorkerThread</strong></a></p></td>
<td align="left"><p>此例程调用的工作线程的上下文中的例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554627" data-raw-source="[&lt;strong&gt;RxpReferenceNetFcb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554627)"><strong>RxpReferenceNetFcb</strong></a></p></td>
<td align="left"><p>此例程递增 FCB 的引用计数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554632" data-raw-source="[&lt;strong&gt;RxPrefixTableLookupName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554632)"><strong>RxPrefixTableLookupName</strong></a></p></td>
<td align="left"><p>例程查找到目录 SRV_CALL 所用的前缀表中的名称和 NET_ROOT 名称，并将从基础指针转换为包含结构。</p>
<p>此例程 RDBSS 供内部使用和不能由网络微型重定向程序驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554637" data-raw-source="[&lt;strong&gt;RxpReleasePrefixTableLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554637)"><strong>RxpReleasePrefixTableLock</strong></a></p></td>
<td align="left"><p>此例程释放对目录 SRV_CALL 和 NET_ROOT 名称所用的前缀表上的锁。</p>
<p>此例程才在 Windows XP 和 Windows 2000 上可用。 此例程 RDBSS 供内部使用和不能由网络微型重定向程序驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554643" data-raw-source="[&lt;strong&gt;RxPrepareContextForReuse&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554643)"><strong>RxPrepareContextForReuse</strong></a></p></td>
<td align="left"><p>此例程准备 RX_CONTEXT 结构以供重复使用通过重置所有特定于操作的分配和所做的收购。 获取从 IRP 的参数不会修改。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554649" data-raw-source="[&lt;strong&gt;RxPrepareToReparseSymbolicLink&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554649)"><strong>RxPrepareToReparseSymbolicLink</strong></a></p></td>
<td align="left"><p>此例程设置文件的对象名称，以便重新分析。 网络微型-重定向程序使用此例程来遍历符号链接。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554655" data-raw-source="[&lt;strong&gt;RxpTrackDereference&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554655)"><strong>RxpTrackDereference</strong></a></p></td>
<td align="left"><p>此例程用于跟踪请求，若要取消引用 SRV_CALL、 NET_ROOT、 V_NET_ROOT、 FOBX、 FCB，并在选中 SRV_OPEN 结构生成。 这些日志取消引用请求的日志记录系统和 WMI 可访问。</p>
<p>对于零售版本，此例程没有任何影响。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554659" data-raw-source="[&lt;strong&gt;RxpTrackReference&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554659)"><strong>RxpTrackReference</strong></a></p></td>
<td align="left"><p>此例程用于跟踪请求以引用 SRV_CALL、 NET_ROOT、 V_NET_ROOT、 FOBX、 FCB，并在选中 SRV_OPEN 结构生成。 可以通过日志记录系统和 WMI 访问的这些引用请求的日志。</p>
<p>对于零售版本，此例程没有任何影响。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554662" data-raw-source="[&lt;strong&gt;RxpUnregisterMinirdr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554662)"><strong>RxpUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>注销 RDBSS 与驱动程序并从内部 RDBSS registration 表中删除注册信息的网络微型重定向程序驱动程序调用该例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554673" data-raw-source="[&lt;strong&gt;RxPurgeAllFobxs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554673)"><strong>RxPurgeAllFobxs</strong></a></p></td>
<td align="left"><p>此例程会清除网络微型重定向与关联的所有 FOBX 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554679" data-raw-source="[&lt;strong&gt;RxPurgeRelatedFobxs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554679)"><strong>RxPurgeRelatedFobxs</strong></a></p></td>
<td align="left"><p>此例程会清除所有与 NET_ROOT 结构相关联的 FOBX 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554686" data-raw-source="[&lt;strong&gt;RxReassociateMid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554686)"><strong>RxReassociateMid</strong></a></p></td>
<td align="left"><p>此例程重新 MID 关联与备用的上下文。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554688" data-raw-source="[&lt;strong&gt;RxReference&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554688)"><strong>RxReference</strong></a></p></td>
<td align="left"><p>此例程递增 RDBSS 所使用的引用计数的数据结构的多个实例上的引用计数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554693" data-raw-source="[&lt;strong&gt;RxRegisterMinirdr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554693)"><strong>RxRegisterMinirdr</strong></a></p></td>
<td align="left"><p>此例程称为网络微型重定向程序驱动程序，该驱动程序注册到 RDBSS，将注册信息添加到内部注册表。 RDBSS 还生成网络微型重定向的设备对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554699" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554699)"><strong>RxReleaseFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>此例程释放使用获取的 FCB 资源<strong>RxAcquireExclusiveFcbResourceInMRx</strong>或<strong>RxAcquireSharedFcbResourceInMRx</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff554694" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceForThreadInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554694)"><strong>RxReleaseFcbResourceForThreadInMRx</strong></a></td>
<td align="left"><p>此例程释放使用获取的 FCB 资源<a href="https://msdn.microsoft.com/library/windows/hardware/ff553375" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553375)"> <strong>RxAcquireSharedFcbResourceInMRxEx</strong></a></p>
<p>Windows Server 2003 Service Pack 1 (SP1) 及更高版本，此例程才可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554701" data-raw-source="[&lt;strong&gt;RxResumeBlockedOperations_Serially&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554701)"><strong>RxResumeBlockedOperations_Serially</strong></a></p></td>
<td align="left"><p>此例程唤醒下一个等待线程，如果有，序列化的阻塞 I/O 队列上。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554707" data-raw-source="[&lt;strong&gt;RxScavengeAllFobxs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554707)"><strong>RxScavengeAllFobxs</strong></a></p></td>
<td align="left"><p>此例程清理所有与给定的网络微型重定向设备对象相关联的 FOBX 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554713" data-raw-source="[&lt;strong&gt;RxScavengeFobxsForNetRoot&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554713)"><strong>RxScavengeFobxsForNetRoot</strong></a></p></td>
<td align="left"><p>此例程清理的所有适用于给定 NET_ROOT 结构 FOBX 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554718" data-raw-source="[&lt;strong&gt;RxSetDomainForMailslotBroadcast&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554718)"><strong>RxSetDomainForMailslotBroadcast</strong></a></p></td>
<td align="left"><p>此例程称为网络微型重定向程序驱动程序，设置用于邮件槽广播 mailslot 的驱动程序支持的域。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554722" data-raw-source="[&lt;strong&gt;RxSetMinirdrCancelRoutine&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554722)"><strong>RxSetMinirdrCancelRoutine</strong></a></p></td>
<td align="left"><p>此例程将设置为 RX_CONTEXT 结构网络微型重定向在取消例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554728" data-raw-source="[&lt;strong&gt;RxSetSrvCallDomainName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554728)"><strong>RxSetSrvCallDomainName</strong></a></p></td>
<td align="left"><p>此例程设置与任何给定的服务器 （SRV_CALL 结构） 关联的域名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554734" data-raw-source="[&lt;strong&gt;RxSpinDownMRxDispatcher&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554734)"><strong>RxSpinDownMRxDispatcher</strong></a></p></td>
<td align="left"><p>此例程卸除网络微型重定向的调度程序上下文。</p>
<p>此例程才适用于 Windows XP 及更高版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554736" data-raw-source="[&lt;strong&gt;RxStartMinirdr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554736)"><strong>RxStartMinirdr</strong></a></p></td>
<td align="left"><p>此例程会启动网络微型重定向的调用以注册其自身。 如果该驱动程序指示对 UNC 名称的支持，RDBSS 还将作为通用命名约定 (UNC) 提供程序与多个 UNC Provider (MUP) 注册网络微型重定向程序驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554743" data-raw-source="[&lt;strong&gt;RxStopMinirdr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554743)"><strong>RxStopMinirdr</strong></a></p></td>
<td align="left"><p>此例程将停止网络微型重定向程序驱动程序。 已停止的驱动程序将不再接受新的命令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554744" data-raw-source="[&lt;strong&gt;RxUnregisterMinirdr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554744)"><strong>RxUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>此例程是内联函数中定义<em>rxstruc.h</em>注销 RDBSS 与驱动程序并从内部 RDBSS registration 表中删除注册信息的网络微型重定向程序驱动程序调用。 <strong>RxUnregisterMinirdr</strong>内联函数在内部调用<strong>RxpUnregisterMinirdr</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557355" data-raw-source="[&lt;strong&gt;_RxAllocatePoolWithTag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557355)"><strong>_RxAllocatePoolWithTag</strong></a></p></td>
<td align="left"><p>此例程会具有四个字节标记可用于帮助捕获实例的内存问题的块的开头的池将分配内存。</p>
<p>建议<strong>RxAllocatePoolWithTag</strong>而不是直接调用该例程使用宏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557358" data-raw-source="[&lt;strong&gt;_RxCheckMemoryBlock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557358)"><strong>_RxCheckMemoryBlock</strong></a></p></td>
<td align="left"><p>此例程将检查的特殊 RX_POOL_HEADER 标头签名的内存块。 请注意，网络微型重定向程序驱动程序将需要此特殊的签名块添加到内存分配才能使用该例程。</p>
<p>由于尚未实现此特殊的标头块，则不应使用此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557363" data-raw-source="[&lt;strong&gt;_RxFreePool&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557363)"><strong>_RxFreePool</strong></a></p></td>
<td align="left"><p>此例程将释放内存池。</p>
<p>建议<strong>RxFreePool</strong>而不是直接调用该例程使用宏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557368" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557368)"><strong>_RxLog</strong></a></p></td>
<td align="left"><p>此例程采用格式字符串和可变数量的参数和设置格式 structureing 的输出字符串，如启用了 I/O 错误日志条目如果日志记录。</p>
<p>建议<a href="https://msdn.microsoft.com/library/windows/hardware/ff557368" data-raw-source="[&lt;strong&gt;RxLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557368)"> <strong>RxLog</strong> </a>而不是直接调用该例程使用宏。</p>
<p>此例程才可用的 Windows Server 2003、 Windows XP 和 Windows 2000 上 RDBSS checked 版本。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557374" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557374)"><strong>__RxFillAndInstallFastIoDispatch</strong></a></p></td>
<td align="left"><p>此例程填写快速 I/O 调度向量为与正常调度 I/O 向量相同，并将其安装到都与传递的设备对象相关联的驱动程序对象。</p>
<p>此例程仅对非整体化驱动程序实现，且不执行任何操作对整体化驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff557377" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperations&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557377)"><strong>__RxSynchronizeBlockingOperations</strong></a></td>
<td align="left"><p>此例程用于同步到相同的工作队列的阻塞 I/O。 此例程是由在内部用于 RDBSS 同步命名的管道的操作。 此例程可能会通过网络微型重定向，用于同步对单独的队列是由网络微型重定向维护操作。</p>
<p>此例程才可在 Windows Server 2003 上。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff557382" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557382)"><strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong></a></td>
<td align="left"><p>此例程用于同步到相同的工作队列的阻塞 I/O。 此例程是由在内部用于 RDBSS 同步命名的管道的操作。 此例程可能会通过网络微型重定向，用于同步对单独的队列是由网络微型重定向维护操作。</p>
<p>此例程才在 Windows XP 和 Windows 2000 上可用。</p></td>
</tr>
</tbody>
</table>

 

 

 




