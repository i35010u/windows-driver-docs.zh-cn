---
title: 引擎的连接管理
description: 引擎的连接管理
ms.assetid: 00ac74c5-2a69-493f-ad9b-6fa2f9082ac1
keywords:
- RDBSS WDK 的文件系统，引擎的连接管理
- 重定向驱动器缓冲子系统 WDK 的文件系统，引擎的连接管理
- 连接引擎 WDK 网络重定向程序
- TDI 驱动程序 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bad704fc0dc11ec9b7bdeeebf918a839cf379ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541522"
---
# <a name="connection-engine-management"></a>引擎的连接管理


## <span id="ddk_connection_engine_management_if"></span><span id="DDK_CONNECTION_ENGINE_MANAGEMENT_IF"></span>


RDBSS，连接引擎被设计来映射和尽可能真实地模拟 TDI 规范。 这提供了充分利用了通过网络微型-重定向程序使用的底层 TDI 实现高效机制。

虽然 RDBSS 连接引擎 does 抽象 TDI，网络重定向程序也是可用来直接与 TDI 而不是使用这些 RDBSS 连接引擎例程进行通信。 为 TDI 提供包装器的现有 RDBSS 连接引擎例程不断问世以支持 Microsoft 网络，因此它们是非常以 Windows 为中心并且可能不是适用于其他网络控制器。 此外，连接引擎例程中 RDBSS 是要从 Windows Server 2003 之后发布的 Windows 操作系统中删除。 将来，每个网络重定向程序将负责开发 （到 TDI 或某些其他传输） 所需的连接引擎例程。 例如，某用户模式下发送程序进程中来发送 HTTP 数据包 (标准 TCP/IP) 而不是 TDI 可以咨询 WebDAV 重定向程序。

RDBSS 连接引擎例程处理以下实体：

-   传输

-   传输地址

-   传输连接

-   在连接上的虚拟线路

传输协议是绑定到任何系统上的各种传输服务提供程序。 传输地址是本地连接终结点。 连接为终结点之间的传输连接。 每个连接封装虚拟线路 （通常一个） 的数。

创建和操作与 RDBSS 相关联的各种连接引擎例程的以下重要的数据结构：

-   RXCE\_传输-封装所有参数为传输

-   RXCE\_地址--封装所有的传输地址的参数

-   RXCE\_连接--封装所有的传输连接的参数

-   RXCE\_VC-封装所有虚拟线路上的传输连接的参数

网络微型重定向程序驱动程序可以使用这些数据结构，并调用为每个类型生成和关闭连接引擎部分提供的例程。 这些例程不执行分配或释放与这些结构相关联的内存。 这提供了灵活的机制来管理这些连接引擎数据结构的实例的最小重定向程序驱动程序。

上面所述的四个连接引擎类型标记的每个数据结构具有特殊 RXCE 开头\_签名由广泛 RDBSS 用于验证的签名。

RDBSS 提供网络微型重定向程序驱动程序可以使用以下连接引擎例程。

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
<td align="left"><p>此例程建立本地 RDBSS 连接地址和给定的远程地址之间的连接，并支持多个传输协议。 指定一组的本地地址，此例程会尝试连接到本地地址与关联的传输的所有目标服务器。 作为入选方，具体取决于连接选项选择一个连接。 必须在系统工作线程的上下文中调用此例程。</p></td>
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
<td align="left"><p>此例程将查询与连接相关的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553474" data-raw-source="[&lt;strong&gt;RxCeQueryTransportInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553474)"><strong>RxCeQueryTransportInformation</strong></a></p></td>
<td align="left"><p>此例程将返回有关的连接数和给定传输的服务质量的传输信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553479" data-raw-source="[&lt;strong&gt;RxCeSend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553479)"><strong>RxCeSend</strong></a></p></td>
<td align="left"><p>此例程将指定的连接沿着 TSDU 发送虚拟线路上。</p></td>
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
</tbody>
</table>

 

**请注意**   TDI 将不支持在 Microsoft Windows 版本在 Windows Vista 后。 使用[Windows 筛选平台](https://msdn.microsoft.com/library/windows/hardware/ff571068)或[Winsock 内核](https://msdn.microsoft.com/library/windows/hardware/ff571083)相反。

 

 

 




