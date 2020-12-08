---
title: RDBSS 提供的例程
description: RDBSS 提供的例程
keywords:
- RDBSS WDK 文件系统，例程
- 重定向的驱动器缓冲子系统 WDK 文件系统、例程
- 例程 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e233b3d938e1e2349fc42a54b65ca2c98a8c9ee5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819577"
---
# <a name="routines-provided-by-rdbss"></a>RDBSS 提供的例程


## <span id="ddk_functions_provided_by_rdbss_if"></span><span id="DDK_FUNCTIONS_PROVIDED_BY_RDBSS_IF"></span>


以下例程由 RDBSS 导出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程所返回的值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquireexclusivefcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxAcquireExclusiveFcbResourceInMRx&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquireexclusivefcbresourceinmrx)"><strong>RxAcquireExclusiveFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>此资源获取例程获取以独占模式 (FCB) 资源的文件控制块。 此例程将等待 FCB 资源空闲，因此在获取资源之前，此例程不会返回控制。 即使与此 FCB 关联的 RX_CONTEXT 已取消，此例程也会获取 FCB 资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRx&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrx)"><strong>RxAcquireSharedFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>此资源获取例程获取共享模式下的 FCB 资源。 如果以前以独占方式获取 FCB 资源，此例程将等待该资源空闲，因此在获取资源之前，此例程不会返回控制。 即使与此 FCB 关联的 RX_CONTEXT 已取消，此例程也会获取 FCB 资源。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex)"><strong>RxAcquireSharedFcbResourceInMRxEx</strong></a></td>
<td align="left"><p>此资源获取例程获取共享模式下的 FCB 资源。 如果以前以独占方式获取了 FCB 资源，此例程将等待该资源释放。 在获取资源之前，此例程不会返回控制。 即使与此 FCB 关联的 RX_CONTEXT 已取消，此例程也会获取 FCB 资源。</p>
<p>此例程仅在 Windows Server 2003 Service Pack 1 (SP1) 和更高版本上可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ifs/rxassert" data-raw-source="[&lt;strong&gt;RxAssert&lt;/strong&gt;](./rxassert.md)"><strong>RxAssert</strong></a></p></td>
<td align="left"><p>如果安装了某个内核调试器，则此例程会将 RDBSS 检查的生成中的断言字符串发送到内核调试器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxassociatecontextwithmid" data-raw-source="[&lt;strong&gt;RxAssociateContextWithMid&lt;/strong&gt;](/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxassociatecontextwithmid)"><strong>RxAssociateContextWithMid</strong></a></p></td>
<td align="left"><p>此例程将提供的不透明上下文与 MID_ATLAS 数据结构中 (MID) 的可用多路复用 ID 相关联。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxcanceltimerrequest" data-raw-source="[&lt;strong&gt;RxCancelTimerRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxcanceltimerrequest)"><strong>RxCancelTimerRequest</strong></a></p></td>
<td align="left"><p>此例程取消计时器请求。 要取消的请求由例程和上下文标识。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceallocateirpwithmdl" data-raw-source="[&lt;strong&gt;RxCeAllocateIrpWithMDL&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceallocateirpwithmdl)"><strong>RxCeAllocateIrpWithMDL</strong></a></p></td>
<td align="left"><p>此例程分配用于连接引擎的 IRP，并将 MDL 与 IRP 关联。</p>
<p>此例程仅适用于 Windows XP。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildaddress" data-raw-source="[&lt;strong&gt;RxCeBuildAddress&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildaddress)"><strong>RxCeBuildAddress</strong></a></p></td>
<td align="left"><p>此例程将传输地址与传输绑定相关联。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildconnection" data-raw-source="[&lt;strong&gt;RxCeBuildConnection&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildconnection)"><strong>RxCeBuildConnection</strong></a></p></td>
<td align="left"><p>此例程在本地 RDBSS 连接地址与给定的远程地址之间建立连接。 应在系统工作线程的上下文中调用此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildconnectionovermultipletransports" data-raw-source="[&lt;strong&gt;RxCeBuildConnectionOverMultipleTransports&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildconnectionovermultipletransports)"><strong>RxCeBuildConnectionOverMultipleTransports</strong></a></p></td>
<td align="left"><p>此例程在本地 RDBSS 连接地址与给定的远程地址之间建立连接，并支持多个传输。 指定了一组本地地址，这一例程尝试使用所有与本地地址关联的传输连接到目标服务器。 根据连接选项，将一个连接选作入选方。 必须在系统工作线程的上下文中调用此例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildtransport" data-raw-source="[&lt;strong&gt;RxCeBuildTransport&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildtransport)"><strong>RxCeBuildTransport</strong></a></p></td>
<td align="left"><p>此例程将 RDBSS 传输绑定到指定的传输名称。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildvc" data-raw-source="[&lt;strong&gt;RxCeBuildVC&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcebuildvc)"><strong>RxCeBuildVC</strong></a></p></td>
<td align="left"><p>此例程将虚拟线路添加到指定连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcecancelconnectrequest" data-raw-source="[&lt;strong&gt;RxCeCancelConnectRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcecancelconnectrequest)"><strong>RxCeCancelConnectRequest</strong></a></p></td>
<td align="left"><p>此例程取消以前发出的连接请求。</p>
<p>请注意，当前未实现此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcefreeirp" data-raw-source="[&lt;strong&gt;RxCeFreeIrp&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcefreeirp)"><strong>RxCeFreeIrp</strong></a></p></td>
<td align="left"><p>此例程释放连接引擎使用的 IRP。</p>
<p>此例程仅适用于 Windows XP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceinitiatevcdisconnect" data-raw-source="[&lt;strong&gt;RxCeInitiateVCDisconnect&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceinitiatevcdisconnect)"><strong>RxCeInitiateVCDisconnect</strong></a></p></td>
<td align="left"><p>此例程在虚拟线路上启动断开连接。 必须在系统工作线程的上下文中调用此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequeryadapterstatus" data-raw-source="[&lt;strong&gt;RxCeQueryAdapterStatus&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequeryadapterstatus)"><strong>RxCeQueryAdapterStatus</strong></a></p></td>
<td align="left"><p>此例程返回给定传输的 ADAPTER_STATUS 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequeryinformation" data-raw-source="[&lt;strong&gt;RxCeQueryInformation&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequeryinformation)"><strong>RxCeQueryInformation</strong></a></p></td>
<td align="left"><p>此例程查询有关给定虚拟线路的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequerytransportinformation" data-raw-source="[&lt;strong&gt;RxCeQueryTransportInformation&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequerytransportinformation)"><strong>RxCeQueryTransportInformation</strong></a></p></td>
<td align="left"><p>此例程查询给定的传输以获取有关连接计数和服务质量的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcesend" data-raw-source="[&lt;strong&gt;RxCeSend&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcesend)"><strong>RxCeSend</strong></a></p></td>
<td align="left"><p>此例程通过虚拟线路上指定的连接 (TSDU) 发送传输服务数据单元。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcesenddatagram" data-raw-source="[&lt;strong&gt;RxCeSendDatagram&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcesenddatagram)"><strong>RxCeSendDatagram</strong></a></p></td>
<td align="left"><p>此例程将 TSDU 发送到指定的传输地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardownaddress" data-raw-source="[&lt;strong&gt;RxCeTearDownAddress&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardownaddress)"><strong>RxCeTearDownAddress</strong></a></p></td>
<td align="left"><p>此例程从传输绑定中删除传输地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardownconnection" data-raw-source="[&lt;strong&gt;RxCeTearDownConnection&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardownconnection)"><strong>RxCeTearDownConnection</strong></a></p></td>
<td align="left"><p>此例程泪水给定的连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardowntransport" data-raw-source="[&lt;strong&gt;RxCeTearDownTransport&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardowntransport)"><strong>RxCeTearDownTransport</strong></a></p></td>
<td align="left"><p>此例程与指定的传输解除绑定。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardownvc" data-raw-source="[&lt;strong&gt;RxCeTearDownVC&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxceteardownvc)"><strong>RxCeTearDownVC</strong></a></p></td>
<td align="left"><p>此例程泪水虚拟连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxchangebufferingstate" data-raw-source="[&lt;strong&gt;RxChangeBufferingState&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxchangebufferingstate)"><strong>RxChangeBufferingState</strong></a></p></td>
<td align="left"><p>调用此例程来处理缓冲状态更改请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest" data-raw-source="[&lt;strong&gt;RxCompleteRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest)"><strong>RxCompleteRequest</strong></a></p></td>
<td align="left"><p>此例程用于完成与 RX_CONTEXT 结构关联的 IRP。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序驱动程序使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest_real" data-raw-source="[&lt;strong&gt;RxCompleteRequest_Real&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest_real)"><strong>RxCompleteRequest_Real</strong></a></p></td>
<td align="left"><p>此例程用于完成与 RX_CONTEXT 结构关联的 IRP。 此例程不应由网络小型重定向程序使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxcreatemidatlas" data-raw-source="[&lt;strong&gt;RxCreateMidAtlas&lt;/strong&gt;](/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxcreatemidatlas)"><strong>RxCreateMidAtlas</strong></a></p></td>
<td align="left"><p>此例程分配 MID_ATLAS 数据结构的新实例，并对其进行初始化。 RDBSS 使用在此数据结构中定义的) 中的多路复用 ID (在此数据结构中定义的一种方式是网络客户端 (小型重定向程序) 并且服务器可以区分任何连接上的并发活动请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatenetfcb" data-raw-source="[&lt;strong&gt;RxCreateNetFcb&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatenetfcb)"><strong>RxCreateNetFcb</strong></a></p></td>
<td align="left"><p>此例程为打开此 FCB 的 NET_ROOT 结构分配、初始化新的 FCB 结构并将其插入到内存中数据结构中。 所分配的结构具有 SRV_OPEN 和 FOBX 结构的空间。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序驱动程序使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatenetfobx" data-raw-source="[&lt;strong&gt;RxCreateNetFobx&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatenetfobx)"><strong>RxCreateNetFobx</strong></a></p></td>
<td align="left"><p>此例程分配、初始化和插入新的文件对象扩展 (FOBX) 结构。 在成功创建操作结束时，网络微型重定向程序应调用此例程以创建 FOBX。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatenetroot" data-raw-source="[&lt;strong&gt;RxCreateNetRoot&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatenetroot)"><strong>RxCreateNetRoot</strong></a></p></td>
<td align="left"><p>此例程生成一个表示 NET_ROOT 结构的节点，并将该名称插入到相关设备对象上的网络名称表中。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxcreaterxcontext" data-raw-source="[&lt;strong&gt;RxCreateRxContext&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxcreaterxcontext)"><strong>RxCreateRxContext</strong></a></p></td>
<td align="left"><p>此例程分配新的 RX_CONTEXT 结构并初始化数据结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatesrvcall" data-raw-source="[&lt;strong&gt;RxCreateSrvCall&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatesrvcall)"><strong>RxCreateSrvCall</strong></a></p></td>
<td align="left"><p>此例程生成一个节点，该节点表示服务器调用上下文，并将该名称插入到由 RDBSS 维护的 net name 表中。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序驱动程序使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatesrvopen" data-raw-source="[&lt;strong&gt;RxCreateSrvOpen&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatesrvopen)"><strong>RxCreateSrvOpen</strong></a></p></td>
<td align="left"><p>此例程分配、初始化新的 SRV_OPEN 结构并将其插入到 RDBSS 使用的内存中数据结构中。 如果必须分配新的结构，则它的 FOBX 结构具有空间。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序驱动程序使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatevnetroot" data-raw-source="[&lt;strong&gt;RxCreateVNetRoot&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxcreatevnetroot)"><strong>RxCreateVNetRoot</strong></a></p></td>
<td align="left"><p>此例程生成一个表示 V_NET_ROOT 结构的节点，并将该名称插入 NET name 表中。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序驱动程序使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ifs/rxdbgbreakpoint" data-raw-source="[&lt;strong&gt;RxDbgBreakPoint&lt;/strong&gt;](./rxdbgbreakpoint.md)"><strong>RxDbgBreakPoint</strong></a></p></td>
<td align="left"><p>如果安装了某个内核调试器，此例程会引发异常;否则，调试系统会对其进行处理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdereference" data-raw-source="[&lt;strong&gt;RxDereference&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdereference)"><strong>RxDereference</strong></a></p></td>
<td align="left"><p>此例程会减少 RDBSS 使用的几个引用计数数据结构实例的引用计数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real" data-raw-source="[&lt;strong&gt;RxDereferenceAndDeleteRxContext_Real&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real)"><strong>RxDereferenceAndDeleteRxContext_Real</strong></a></p></td>
<td align="left"><p>此例程取消引用 RX_CONTEXT 结构，如果引用计数变为零，则它会从 RDBSS 内存中数据结构中解除分配并删除指定的 RX_CONTEXT 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxdestroymidatlas" data-raw-source="[&lt;strong&gt;RxDestroyMidAtlas&lt;/strong&gt;](/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxdestroymidatlas)"><strong>RxDestroyMidAtlas</strong></a></p></td>
<td align="left"><p>此例程销毁 MID_ATLAS 数据结构的现有实例，并释放已分配的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxdispatchtoworkerthread" data-raw-source="[&lt;strong&gt;RxDispatchToWorkerThread&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxdispatchtoworkerthread)"><strong>RxDispatchToWorkerThread</strong></a></p></td>
<td align="left"><p>此例程在工作线程的上下文中调用例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdriverentry" data-raw-source="[&lt;strong&gt;RxDriverEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdriverentry)"><strong>RxDriverEntry</strong></a></p></td>
<td align="left"><p>此例程由其 <strong>DriverEntry</strong> 中的单一网络小型重定向程序驱动程序调用，用于初始化 RDBSS。</p>
<p>对于非单片驱动程序，此初始化例程等效于<em>rdbss.sys</em>设备驱动程序的<strong>DriverEntry</strong>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfinalizeconnection" data-raw-source="[&lt;strong&gt;RxFinalizeConnection&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfinalizeconnection)"><strong>RxFinalizeConnection</strong></a></p></td>
<td align="left"><p>此例程将删除与共享的连接。 连接上打开的任何文件都将关闭，具体取决于指定的强制级别。 出于性能原因，网络小型重定向程序可能会选择保持打开传输连接，除非指定了某些选项来强制关闭连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfinalizenetfcb" data-raw-source="[&lt;strong&gt;RxFinalizeNetFcb&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfinalizenetfcb)"><strong>RxFinalizeNetFcb</strong></a></p></td>
<td align="left"><p>此例程将完成给定的 FCB 结构。 调用方必须在与 FCB 关联的 NET_ROOT 结构上具有排他锁。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序驱动程序使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizenetfobx" data-raw-source="[&lt;strong&gt;RxFinalizeNetFobx&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizenetfobx)"><strong>RxFinalizeNetFobx</strong></a></p></td>
<td align="left"><p>此例程将完成给定的 FOBX 结构。 调用方必须在与此 FOBX 关联的 FCB 上有一个排他锁。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizenetroot" data-raw-source="[&lt;strong&gt;RxFinalizeNetRoot&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizenetroot)"><strong>RxFinalizeNetRoot</strong></a></p></td>
<td align="left"><p>此例程将完成给定的 NET_ROOT 结构。 调用方应对与此 NET_ROOT 结构关联的设备对象的网络名称表上的锁进行独占访问， (通过 SRV_CALL 结构) 。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序驱动程序使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizesrvcall" data-raw-source="[&lt;strong&gt;RxFinalizeSrvCall&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizesrvcall)"><strong>RxFinalizeSrvCall</strong></a></p></td>
<td align="left"><p>此例程将完成给定的 SRV_CALL 结构。 调用方应具有对与此 SRV_CALL 结构关联的设备对象的网络名称表上的锁的独占访问权限。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序驱动程序使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizesrvopen" data-raw-source="[&lt;strong&gt;RxFinalizeSrvOpen&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizesrvopen)"><strong>RxFinalizeSrvOpen</strong></a></p></td>
<td align="left"><p>此例程将完成给定的 SRV_OPEN 结构。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序驱动程序使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizevnetroot" data-raw-source="[&lt;strong&gt;RxFinalizeVNetRoot&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinalizevnetroot)"><strong>RxFinalizeVNetRoot</strong></a></p></td>
<td align="left"><p>此例程将完成给定的 V_NET_ROOT 结构。 调用方必须以独占方式访问与此 V_NET_ROOT 结构关联的设备对象的网络名称表上的锁。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinishfcbinitialization" data-raw-source="[&lt;strong&gt;RxFinishFcbInitialization&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxfinishfcbinitialization)"><strong>RxFinishFcbInitialization</strong></a></p></td>
<td align="left"><p>此例程用于在网络最小化重定向器成功完成创建操作后完成 FCB 的初始化。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxforcefinalizeallvnetroots" data-raw-source="[&lt;strong&gt;RxForceFinalizeAllVNetRoots&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxforcefinalizeallvnetroots)"><strong>RxForceFinalizeAllVNetRoots</strong></a></p></td>
<td align="left"><p>此例程强制终结与给定 NET_ROOT 结构关联的所有 V_NET_ROOT 结构。 调用方必须以独占方式访问与此 V_NET_ROOT 结构关联的设备对象的网络名称表上的锁。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-rxfsddispatch" data-raw-source="[&lt;strong&gt;RxFsdDispatch&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxfsddispatch)"><strong>RxFsdDispatch</strong></a></p></td>
<td align="left"><p>此例程实现 (FSD 的文件系统驱动程序) 调度，以便 RDBSS 处理 i/o 请求数据包 (IRP) 。 此例程由驱动程序调度例程中的网络微重定向器调用，以启动 RDBSS 处理请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest" data-raw-source="[&lt;strong&gt;RxFsdPostRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest)"><strong>RxFsdPostRequest</strong></a></p></td>
<td align="left"><p>此例程将 RX_CONTEXT 结构指定的 i/o 请求数据包 (IRP) 到辅助队列中，以便文件系统进程 (FSP) 进行处理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxgetfilesizewithlock" data-raw-source="[&lt;strong&gt;RxGetFileSizeWithLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxgetfilesizewithlock)"><strong>RxGetFileSizeWithLock</strong></a></p></td>
<td align="left"><p>此例程使用锁定获取 FCB 结构中的文件大小，以确保以一致的方式读取64位值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxgetrdbssprocess" data-raw-source="[&lt;strong&gt;RxGetRDBSSProcess&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxgetrdbssprocess)"><strong>RxGetRDBSSProcess</strong></a></p></td>
<td align="left"><p>此例程返回一个指针，该指针指向 RDBSS 内核进程使用的主线程的进程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstate" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingState&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstate)"><strong>RxIndicateChangeOfBufferingState</strong></a></p></td>
<td align="left"><p>调用此例程来注册 (oplock 中断指示的缓冲状态更改请求，例如) 以便以后处理。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstateforsrvopen" data-raw-source="[&lt;strong&gt;RxIndicateChangeOfBufferingStateForSrvOpen&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxindicatechangeofbufferingstateforsrvopen)"><strong>RxIndicateChangeOfBufferingStateForSrvOpen</strong></a></p></td>
<td align="left"><p>调用此例程来注册 (oplock 中断指示的缓冲状态更改请求，例如) 以便以后处理。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxinferfiletype" data-raw-source="[&lt;strong&gt;RxInferFileType&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxinferfiletype)"><strong>RxInferFileType</strong></a></p></td>
<td align="left"><p>此例程尝试从 RX_CONTEXT 结构中的 <strong>CreateOptions</strong> ( <strong>CreateOptions</strong>) 字段推断文件类型 (directory 或非目录) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxinitializecontext" data-raw-source="[&lt;strong&gt;RxInitializeContext&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxinitializecontext)"><strong>RxInitializeContext</strong></a></p></td>
<td align="left"><p>此例程初始化新分配的 RX_CONTEXT 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxisthisacscagentopen" data-raw-source="[&lt;strong&gt;RxIsThisACscAgentOpen&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxisthisacscagentopen)"><strong>RxIsThisACscAgentOpen</strong></a></p></td>
<td align="left"><p>此例程确定用户模式的客户端缓存代理是否打开了文件。</p>
<p>此例程只能在 Windows Server 2003 上使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlockenumerator" data-raw-source="[&lt;strong&gt;RxLockEnumerator&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlockenumerator)"><strong>RxLockEnumerator</strong></a></p></td>
<td align="left"><p>此例程是从网络小型重定向程序调用的，用于枚举 FCB 上的文件锁定。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect)"><strong>RxLogEventDirect</strong></a></p></td>
<td align="left"><p>调用此例程以便向 i/o 错误日志记录错误。 建议使用 <strong>RxLogEvent</strong> 或 <strong>RxLogFailure</strong> 宏，而不是直接调用此例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithannotation" data-raw-source="[&lt;strong&gt;RxLogEventWithAnnotation&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithannotation)"><strong>RxLogEventWithAnnotation</strong></a></p></td>
<td align="left"><p>此例程分配 i/o 错误日志结构，填充日志结构，并将此结构写入 i/o 错误日志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect)"><strong>RxLogEventWithBufferDirect</strong></a></p></td>
<td align="left"><p>调用此例程可将错误记录到 i/o 错误日志。 此例程将行号和状态编码为存储在 i/o 错误日志结构中的数据缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiocompletion" data-raw-source="[&lt;strong&gt;RxLowIoCompletion&lt;/strong&gt;](/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiocompletion)"><strong>RxLowIoCompletion</strong></a></p></td>
<td align="left"><p>当处理完成时，如果最初返回 "挂起"，则在处理完成时，必须由网络微型重定向程序驱动程序的低 i/o 例程调用此例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiogetbufferaddress" data-raw-source="[&lt;strong&gt;RxLowIoGetBufferAddress&lt;/strong&gt;](/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiogetbufferaddress)"><strong>RxLowIoGetBufferAddress</strong></a></p></td>
<td align="left"><p>此例程返回与 RX_CONTEXT 结构的 <strong>LowIoContext</strong> 结构中的 MDL 相对应的缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-rxmakelatedeviceavailable" data-raw-source="[&lt;strong&gt;RxMakeLateDeviceAvailable&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxmakelatedeviceavailable)"><strong>RxMakeLateDeviceAvailable</strong></a></p></td>
<td align="left"><p>此例程修改设备对象以使 "延迟设备" 可用。 "后期" 设备是指不在驱动程序的加载例程中创建的设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext" data-raw-source="[&lt;strong&gt;RxMapAndDissociateMidFromContext&lt;/strong&gt;](/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapanddissociatemidfromcontext)"><strong>RxMapAndDissociateMidFromContext</strong></a></p></td>
<td align="left"><p>此例程在 MID_ATLAS 的数据结构中将 MID 映射到其关联的上下文，并将中间与上下文解除关联。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapmidtocontext" data-raw-source="[&lt;strong&gt;RxMapMidToContext&lt;/strong&gt;](/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxmapmidtocontext)"><strong>RxMapMidToContext</strong></a></p></td>
<td align="left"><p>此例程在 MID_ATLAS 数据结构中将 MID 映射到其关联的上下文。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxmapsystembuffer" data-raw-source="[&lt;strong&gt;RxMapSystemBuffer&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxmapsystembuffer)"><strong>RxMapSystemBuffer</strong></a></p></td>
<td align="left"><p>此例程返回 i/o 请求数据包 (IRP) 的系统缓冲区地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheactivateentry" data-raw-source="[&lt;strong&gt;RxNameCacheActivateEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheactivateentry)"><strong>RxNameCacheActivateEntry</strong></a></p></td>
<td align="left"><p>此例程采用名称缓存条目，并更新过期时间和网络小型重定向程序上下文。 然后，它会将该条目置于活动列表中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecheckentry" data-raw-source="[&lt;strong&gt;RxNameCacheCheckEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecheckentry)"><strong>RxNameCacheCheckEntry</strong></a></p></td>
<td align="left"><p>此例程检查 NAME_CACHE 项的有效性。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecreateentry" data-raw-source="[&lt;strong&gt;RxNameCacheCreateEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachecreateentry)"><strong>RxNameCacheCreateEntry</strong></a></p></td>
<td align="left"><p>此例程分配并初始化具有给定名称字符串的 NAME_CACHE 结构。 预计调用方将初始化名称缓存上下文的任何其他网络微重定向器元素，然后将该条目放入 "名称缓存活动" 列表中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentry" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentry)"><strong>RxNameCacheExpireEntry</strong></a></p></td>
<td align="left"><p>此例程为可用列表中的 NAME_CACHE 条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentrywithshortname" data-raw-source="[&lt;strong&gt;RxNameCacheExpireEntryWithShortName&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheexpireentrywithshortname)"><strong>RxNameCacheExpireEntryWithShortName</strong></a></p></td>
<td align="left"><p>此例程会使名称前缀与给定短文件名匹配的所有 NAME_CACHE 项过期。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefetchentry" data-raw-source="[&lt;strong&gt;RxNameCacheFetchEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefetchentry)"><strong>RxNameCacheFetchEntry</strong></a></p></td>
<td align="left"><p>此例程查找 NAME_CACHE 条目的指定名称字符串匹配项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefinalize" data-raw-source="[&lt;strong&gt;RxNameCacheFinalize&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefinalize)"><strong>RxNameCacheFinalize</strong></a></p></td>
<td align="left"><p>此例程将释放与 NAME_CACHE_CONTROL 结构关联的所有 NAME_CACHE 项的存储。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefreeentry" data-raw-source="[&lt;strong&gt;RxNameCacheFreeEntry&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecachefreeentry)"><strong>RxNameCacheFreeEntry</strong></a></p></td>
<td align="left"><p>此例程会释放 NAME_CACHE 项的存储并减少与 NAME_CACHE_CONTROL 结构关联的 NAME_CACHE 缓存项的计数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheinitialize" data-raw-source="[&lt;strong&gt;RxNameCacheInitialize&lt;/strong&gt;](/windows-hardware/drivers/ddi/namcache/nf-namcache-rxnamecacheinitialize)"><strong>RxNameCacheInitialize</strong></a></p></td>
<td align="left"><p>此例程初始化 NAME_CACHE 结构并将其与 NAME_CACHE_CONTROL 结构关联。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ifs/rxnewmapuserbuffer" data-raw-source="[&lt;strong&gt;RxNewMapUserBuffer&lt;/strong&gt;](./rxnewmapuserbuffer.md)"><strong>RxNewMapUserBuffer</strong></a></p></td>
<td align="left"><p>此例程返回用于低 i/o 的用户缓冲区的地址。</p>
<p>此例程仅适用于 Windows XP 和 Windows 2000。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockexclusive" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockExclusive&lt;/strong&gt;](/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockexclusive)"><strong>RxpAcquirePrefixTableLockExclusive</strong></a></p></td>
<td align="left"><p>此例程获取用于目录 SRV_CALL 和 NET_ROOT 名称的前缀表的排他锁。</p>
<p>此例程仅适用于 Windows XP 和 Windows 2000。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockshared" data-raw-source="[&lt;strong&gt;RxpAcquirePrefixTableLockShared&lt;/strong&gt;](/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpacquireprefixtablelockshared)"><strong>RxpAcquirePrefixTableLockShared</strong></a></p></td>
<td align="left"><p>此例程获取用于目录 SRV_CALL 和 NET_ROOT 名称的前缀表上的共享锁。</p>
<p>此例程仅适用于 Windows XP 和 Windows 2000。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序驱动程序使用。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpdereferenceandfinalizenetfcb" data-raw-source="[&lt;strong&gt;RxpDereferenceAndFinalizeNetFcb&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpdereferenceandfinalizenetfcb)"><strong>RxpDereferenceAndFinalizeNetFcb</strong></a></td>
<td align="left"><p>此例程取消引用引用计数并完成 FCB。</p>
<p>此例程仅在 Windows Server 2003 Service Pack 1 (SP1) 和更高版本上可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpdereferencenetfcb" data-raw-source="[&lt;strong&gt;RxpDereferenceNetFcb&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpdereferencenetfcb)"><strong>RxpDereferenceNetFcb</strong></a></p></td>
<td align="left"><p>此例程递减 FCB 上的引用计数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostoneshottimerrequest" data-raw-source="[&lt;strong&gt;RxPostOneShotTimerRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostoneshottimerrequest)"><strong>RxPostOneShotTimerRequest</strong></a></p></td>
<td align="left"><p>驱动程序使用此例程来初始化一次拍摄计时器请求。 当计时器过期时，传递给此例程的工作线程例程将被调用一次。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostrecurrenttimerrequest" data-raw-source="[&lt;strong&gt;RxPostRecurrentTimerRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostrecurrenttimerrequest)"><strong>RxPostRecurrentTimerRequest</strong></a></p></td>
<td align="left"><p>此例程用于初始化重复性计时器请求。 当重复性计时器根据此例程的输入参数触发时，传递给此例程的工作线程例程会定期调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxposttoworkerthread" data-raw-source="[&lt;strong&gt;RxPostToWorkerThread&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxposttoworkerthread)"><strong>RxPostToWorkerThread</strong></a></p></td>
<td align="left"><p>此例程在工作线程的上下文中调用例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpreferencenetfcb" data-raw-source="[&lt;strong&gt;RxpReferenceNetFcb&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxpreferencenetfcb)"><strong>RxpReferenceNetFcb</strong></a></p></td>
<td align="left"><p>此例程将增加 FCB 上的引用计数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/prefix/nf-prefix-rxprefixtablelookupname" data-raw-source="[&lt;strong&gt;RxPrefixTableLookupName&lt;/strong&gt;](/windows-hardware/drivers/ddi/prefix/nf-prefix-rxprefixtablelookupname)"><strong>RxPrefixTableLookupName</strong></a></p></td>
<td align="left"><p>此例程在前缀表中查找用于目录 SRV_CALL 和 NET_ROOT 名称的名称，并将基础指针转换为包含结构。</p>
<p>此例程由 RDBSS 在内部使用，不应由网络微型重定向程序驱动程序使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpreleaseprefixtablelock" data-raw-source="[&lt;strong&gt;RxpReleasePrefixTableLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/prefix/nf-prefix-rxpreleaseprefixtablelock)"><strong>RxpReleasePrefixTableLock</strong></a></p></td>
<td align="left"><p>此例程在用于目录 SRV_CALL 和 NET_ROOT 名称的前缀表上释放锁。</p>
<p>此例程仅适用于 Windows XP 和 Windows 2000。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序驱动程序使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxpreparecontextforreuse" data-raw-source="[&lt;strong&gt;RxPrepareContextForReuse&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxpreparecontextforreuse)"><strong>RxPrepareContextForReuse</strong></a></p></td>
<td align="left"><p>此例程通过重置所有特定于操作的分配以及已进行的收购，来准备 RX_CONTEXT 结构以供重用。 不会修改从 IRP 获取的参数。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxpreparetoreparsesymboliclink" data-raw-source="[&lt;strong&gt;RxPrepareToReparseSymbolicLink&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxpreparetoreparsesymboliclink)"><strong>RxPrepareToReparseSymbolicLink</strong></a></p></td>
<td align="left"><p>此例程将设置文件对象名称以方便进行重新分析。 网络小型重定向器使用此例程遍历符号链接。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackdereference" data-raw-source="[&lt;strong&gt;RxpTrackDereference&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackdereference)"><strong>RxpTrackDereference</strong></a></p></td>
<td align="left"><p>此例程用于跟踪在已检查生成中取消引用 SRV_CALL、NET_ROOT、V_NET_ROOT、FOBX、FCB 和 SRV_OPEN 结构的请求。 日志记录系统和 WMI 可访问这些取消引用请求的日志。</p>
<p>对于零售版本，此例程不执行任何操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackreference" data-raw-source="[&lt;strong&gt;RxpTrackReference&lt;/strong&gt;](/windows-hardware/drivers/ddi/fcb/nf-fcb-rxptrackreference)"><strong>RxpTrackReference</strong></a></p></td>
<td align="left"><p>此例程用于跟踪请求，以在检查的生成中引用 SRV_CALL、NET_ROOT、V_NET_ROOT、FOBX、FCB 和 SRV_OPEN 结构。 日志记录系统和 WMI 可访问这些引用请求的日志。</p>
<p>对于零售版本，此例程不执行任何操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-rxpunregisterminirdr" data-raw-source="[&lt;strong&gt;RxpUnregisterMinirdr&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxpunregisterminirdr)"><strong>RxpUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>此例程由网络微型重定向程序驱动程序调用，以使用 RDBSS 注销驱动程序，并从内部 RDBSS 注册表中删除注册信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxpurgeallfobxs" data-raw-source="[&lt;strong&gt;RxPurgeAllFobxs&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxpurgeallfobxs)"><strong>RxPurgeAllFobxs</strong></a></p></td>
<td align="left"><p>此例程会清除与网络小型重定向程序相关的所有 FOBX 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxpurgerelatedfobxs" data-raw-source="[&lt;strong&gt;RxPurgeRelatedFobxs&lt;/strong&gt;](/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxpurgerelatedfobxs)"><strong>RxPurgeRelatedFobxs</strong></a></p></td>
<td align="left"><p>此例程将清除与 NET_ROOT 结构关联的所有 FOBX 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxreassociatemid" data-raw-source="[&lt;strong&gt;RxReassociateMid&lt;/strong&gt;](/windows-hardware/drivers/ddi/midatlax/nf-midatlax-rxreassociatemid)"><strong>RxReassociateMid</strong></a></p></td>
<td align="left"><p>此例程通过备用上下文将了中间。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxreference" data-raw-source="[&lt;strong&gt;RxReference&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxreference)"><strong>RxReference</strong></a></p></td>
<td align="left"><p>此例程将增加 RDBSS 使用的几个引用计数数据结构实例的引用计数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr" data-raw-source="[&lt;strong&gt;RxRegisterMinirdr&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)"><strong>RxRegisterMinirdr</strong></a></p></td>
<td align="left"><p>此例程由网络微重定向程序驱动程序调用，用于向 RDBSS 注册驱动程序，这会将注册信息添加到内部注册表。 RDBSS 还为网络小型重定向程序构建设备对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceInMRx&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceinmrx)"><strong>RxReleaseFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>此例程释放使用 <strong>RxAcquireExclusiveFcbResourceInMRx</strong> 或 <strong>RXACQUIRESHAREDFCBRESOURCEINMRX</strong>获取的 FCB 资源。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceForThreadInMRx&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)"><strong>RxReleaseFcbResourceForThreadInMRx</strong></a></td>
<td align="left"><p>此例程释放使用 RxAcquireSharedFcbResourceInMRxEx 获取的 FCB <a href="/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex)"> <strong>RxAcquireSharedFcbResourceInMRxEx</strong>资源</a></p>
<p>此例程仅在 Windows Server 2003 Service Pack 1 (SP1) 和更高版本上可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially" data-raw-source="[&lt;strong&gt;RxResumeBlockedOperations_Serially&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially)"><strong>RxResumeBlockedOperations_Serially</strong></a></p></td>
<td align="left"><p>此例程唤醒序列化阻塞 i/o 队列上的下一个等待线程（如果有）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxscavengeallfobxs" data-raw-source="[&lt;strong&gt;RxScavengeAllFobxs&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxscavengeallfobxs)"><strong>RxScavengeAllFobxs</strong></a></p></td>
<td align="left"><p>此例程将清除与给定的网络微重定向程序设备对象相关联的所有 FOBX 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxscavengefobxsfornetroot" data-raw-source="[&lt;strong&gt;RxScavengeFobxsForNetRoot&lt;/strong&gt;](/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxscavengefobxsfornetroot)"><strong>RxScavengeFobxsForNetRoot</strong></a></p></td>
<td align="left"><p>此例程将清除与给定 NET_ROOT 结构相关的所有 FOBX 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-rxsetdomainformailslotbroadcast" data-raw-source="[&lt;strong&gt;RxSetDomainForMailslotBroadcast&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxsetdomainformailslotbroadcast)"><strong>RxSetDomainForMailslotBroadcast</strong></a></p></td>
<td align="left"><p>如果驱动程序支持 mailslots，则网络微型重定向程序驱动程序将调用此例程来设置用于 mailslot 广播的域。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxsetminirdrcancelroutine" data-raw-source="[&lt;strong&gt;RxSetMinirdrCancelRoutine&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxsetminirdrcancelroutine)"><strong>RxSetMinirdrCancelRoutine</strong></a></p></td>
<td align="left"><p>此例程为 RX_CONTEXT 结构设置网络微重定向器取消例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxsetsrvcalldomainname" data-raw-source="[&lt;strong&gt;RxSetSrvCallDomainName&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxsetsrvcalldomainname)"><strong>RxSetSrvCallDomainName</strong></a></p></td>
<td align="left"><p>此例程会将与任何给定服务器关联的域名设置 (SRV_CALL 结构的) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxspindownmrxdispatcher" data-raw-source="[&lt;strong&gt;RxSpinDownMRxDispatcher&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxspindownmrxdispatcher)"><strong>RxSpinDownMRxDispatcher</strong></a></p></td>
<td align="left"><p>此例程泪水关闭网络小型重定向程序的调度程序上下文。</p>
<p>此例程仅适用于 Windows XP 和更高版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstartminirdr" data-raw-source="[&lt;strong&gt;RxStartMinirdr&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstartminirdr)"><strong>RxStartMinirdr</strong></a></p></td>
<td align="left"><p>此例程启动一个网络微型重定向程序，调用它来注册自身。 如果驱动程序指示支持 UNC 名称，RDBSS 还会将网络小型重定向器驱动程序注册为具有多 UNC 提供)  (程序的 (UNC) 提供程序的通用命名约定。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr" data-raw-source="[&lt;strong&gt;RxStopMinirdr&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr)"><strong>RxStopMinirdr</strong></a></p></td>
<td align="left"><p>此例程停止网络微型重定向程序驱动程序。 已停止的驱动程序将不再接受新命令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxunregisterminirdr" data-raw-source="[&lt;strong&gt;RxUnregisterMinirdr&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxunregisterminirdr)"><strong>RxUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>此例程是 <em>rxstruc</em> 中定义的内联函数，由网络微型重定向程序驱动程序调用，用于通过 RDBSS 注销驱动程序并从内部 RDBSS 注册表中删除注册信息。 <strong>RxUnregisterMinirdr</strong>内联函数在内部调用<strong>RxpUnregisterMinirdr</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ifs/-rxallocatepoolwithtag" data-raw-source="[&lt;strong&gt;_RxAllocatePoolWithTag&lt;/strong&gt;](./-rxallocatepoolwithtag.md)"><strong>_RxAllocatePoolWithTag</strong></a></p></td>
<td align="left"><p>此例程从池中分配具有四个字节标记的池中的内存，该标记可用于帮助捕获内存问题的实例。</p>
<p>建议使用 <strong>RxAllocatePoolWithTag</strong> 宏，而不是直接调用此例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ifs/-rxcheckmemoryblock" data-raw-source="[&lt;strong&gt;_RxCheckMemoryBlock&lt;/strong&gt;](./-rxcheckmemoryblock.md)"><strong>_RxCheckMemoryBlock</strong></a></p></td>
<td align="left"><p>此例程检查内存块中是否有特殊 RX_POOL_HEADER 的标头签名。 请注意，网络小型重定向器驱动程序需要将此特殊的签名块添加到分配的内存，以便使用该例程。</p>
<p>不应使用此例程，因为尚未实现此特殊标头块。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ifs/-rxfreepool" data-raw-source="[&lt;strong&gt;_RxFreePool&lt;/strong&gt;](./-rxfreepool.md)"><strong>_RxFreePool</strong></a></p></td>
<td align="left"><p>此例程释放内存池。</p>
<p>建议使用 <strong>RxFreePool</strong> 宏，而不是直接调用此例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog)"><strong>_RxLog</strong></a></p></td>
<td align="left"><p>如果启用了日志记录，则此例程采用格式字符串和可变数量的参数并设置 structureing 的输出字符串的格式。</p>
<p>建议使用 <a href="/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;RxLog&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog)"><strong>RxLog</strong></a> 宏，而不是直接调用此例程。</p>
<p>此例程仅适用于在 Windows Server 2003、Windows XP 和 Windows 2000 上的 RDBSS 的已检查版本。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch)"><strong>__RxFillAndInstallFastIoDispatch</strong></a></p></td>
<td align="left"><p>此例程使用正常调度 i/o 向量完全相同的 i/o 调度向量，并将其安装到与传递的设备对象关联的驱动程序对象中。</p>
<p>此例程仅针对非单片驱动程序实现，不在单一驱动程序上执行任何操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperations&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations)"><strong>__RxSynchronizeBlockingOperations</strong></a></td>
<td align="left"><p>此例程用于将阻塞的 i/o 同步到相同的工作队列。 此例程由 RDBSS 在内部使用，用于同步命名管道操作。 网络小型重定向程序可能会使用此例程来同步网络小型重定向程序维护的单独队列上的操作。</p>
<p>此例程只能在 Windows Server 2003 上使用。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock&lt;/strong&gt;](./--rxsynchronizeblockingoperationsmaybedroppingfcblock.md)"><strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong></a></td>
<td align="left"><p>此例程用于将阻塞的 i/o 同步到相同的工作队列。 此例程由 RDBSS 在内部使用，用于同步命名管道操作。 网络小型重定向程序可能会使用此例程来同步网络小型重定向程序维护的单独队列上的操作。</p>
<p>此例程仅适用于 Windows XP 和 Windows 2000。</p></td>
</tr>
</tbody>
</table>

 

