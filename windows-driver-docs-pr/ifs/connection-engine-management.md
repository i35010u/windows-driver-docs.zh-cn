---
title: 连接引擎管理
description: 连接引擎管理
keywords:
- RDBSS WDK 文件系统，连接引擎管理
- 重定向驱动器缓冲子系统 WDK 文件系统、连接引擎管理
- 连接引擎 WDK 网络重定向器
- TDI 驱动程序 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be2ee7b26a6d6f71be5f8f3009912dec8d06798b
ms.sourcegitcommit: 24d316087a8f36ebec9ce33f230004b826a881c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2021
ms.locfileid: "105635113"
---
# <a name="connection-engine-management"></a>连接引擎管理


## <span id="ddk_connection_engine_management_if"></span><span id="DDK_CONNECTION_ENGINE_MANAGEMENT_IF"></span>


在 RDBSS 中，连接引擎旨在尽可能地映射和模拟 TDI 规范。 这提供了一种有效的机制，该机制充分利用了网络小型重定向器使用的底层 TDI 实现。

尽管 RDBSS 连接引擎的确抽象 TDI，但网络重定向器还可以自由地与 TDI 直接通信，而不是使用这些 RDBSS 连接引擎例程。 为 TDI 提供包装的现有 RDBSS 连接引擎例程是为了支持 Microsoft 网络而开发的，因此它们是以 Windows 为中心的，可能不适用于其他网络控制器。 此外，RDBSS 中的连接引擎例程将从 Windows Server 2003 之后发布的 Windows 操作系统中删除。 将来，每个网络重定向程序将负责开发 (TDI 或其他) 传输所需的连接引擎例程。 例如，WebDAV 重定向程序可能会与某些用户模式反射器进行通信，以便 (标准 TCP/IP) 而不是 TDI 来发送 HTTP 数据包。

RDBSS 连接引擎例程处理以下实体：

-   传输

-   传输地址

-   传输连接

-   连接上的虚拟电路

传输是在任何系统上绑定到各种传输服务提供程序的。 传输地址是本地连接终结点。 连接是终结点之间的传输连接。 每个连接都封装了许多虚电路 (通常是一个) 。

以下重要的数据结构由与 RDBSS 关联的各种连接引擎例程创建和操作：

-   RXCE \_ transport--封装传输的所有参数

-   RXCE \_ 地址--封装传输地址的所有参数

-   RXCE \_ 连接--封装传输连接的所有参数

-   RXCE \_ VC--封装传输连接上虚拟线路的所有参数

网络小型重定向程序驱动程序可以使用这些数据结构并调用为每种类型提供的例程来构建和细分连接引擎部分。 这些例程不分配或释放与这些结构关联的内存。 这为迷你重定向器驱动程序提供了一种灵活的机制，用于管理这些连接引擎数据结构的实例。

上面所述的四个连接引擎类型都在每个数据结构的开头标记，该 \_ 签名由 RDBSS 广泛使用，用于验证。

RDBSS 提供了可由网络微型重定向程序驱动程序使用的以下连接引擎例程。

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
<td align="left"><p>此例程在本地 RDBSS 连接地址与给定的远程地址之间建立连接，并支持多个传输。 指定了一组本地地址，这一例程尝试通过与本地地址相关联的所有传输连接到目标服务器。 根据连接选项，将一个连接选作入选方。 必须在系统工作线程的上下文中调用此例程。</p></td>
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
<td align="left"><p>此例程查询有关连接的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequerytransportinformation" data-raw-source="[&lt;strong&gt;RxCeQueryTransportInformation&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcequerytransportinformation)"><strong>RxCeQueryTransportInformation</strong></a></p></td>
<td align="left"><p>此例程返回有关给定传输的连接计数和服务质量的传输信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcesend" data-raw-source="[&lt;strong&gt;RxCeSend&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxce/nf-rxce-rxcesend)"><strong>RxCeSend</strong></a></p></td>
<td align="left"><p>此例程沿虚拟线路上的指定连接发送 TSDU。</p></td>
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
</tbody>
</table>

 

**注意**   Windows Vista 之后的 Microsoft Windows 版本不支持 TDI。 请改用 [Windows 筛选平台](../network/introduction-to-windows-filtering-platform-callout-drivers.md) 或 [Winsock 内核](/windows-hardware/drivers/ddi/_netvista/) 。

 

