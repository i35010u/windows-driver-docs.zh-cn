---
title: SIO_LOOPBACK_FAST_PATH 控制代码
description: SIO_LOOPBACK_FAST_PATH 套接字 I/O 控制代码允许 WSK 的应用程序配置 TCP 套接字的环回接口上更快的操作。
ms.assetid: 5A5AD945-9EFD-4157-AFA4-F9C3995B7C43
ms.date: 08/08/2017
keywords: -SIO_LOOPBACK_FAST_PATH 控制代码与 Windows Vista 一起启动的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 172c07a24ceaa78e3d45fe9013a6bf0f8bc76e96
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379161"
---
# <a name="sioloopbackfastpath-control-code"></a>SIO\_环回\_快速\_路径控制代码


**重要**   **SIO\_环回\_快速\_路径**已弃用，并且不建议在代码中使用。

 

**SIO\_环回\_快速\_路径**套接字 I/O 控制代码允许 WSK 的应用程序配置 TCP 套接字的环回接口上更快的操作。

若要使用此 IOCTL，WSK 应用程序调用[ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)使用以下参数的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskIoctl</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p><strong>SIO_LOOPBACK_FAST_PATH</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>以字节为单位，输入缓冲区的大小。</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向输入缓冲区的指针。 此参数包含一个指向<strong>布尔</strong>值，该值指示是否套接字应该配置为快速 loopback 操作。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p><strong>NULL</strong></p></td>
</tr>
<tr class="odd">
<td><p>Irp</p></td>
<td><p>指向 IRP 的指针。</p></td>
</tr>
</tbody>
</table>

 

应用程序可以使用**SIO\_环回\_快速\_路径**IOCTL，以提高针对 TCP 套接字的 loopback 操作的性能。 此 IOCTL 请求 TCP/IP 堆栈的 loopback 操作的此套接字使用特殊的快速路径。 **SIO\_环回\_快速\_路径**IOCTL 可以仅可用于 TCP 套接字。 在环回会话的两端必须采用此 IOCTL。 使用的 IPv4 或 IPv6 环回接口支持 TCP 环回快速路径。

计划来启动连接请求的套接字必须在发出连接请求之前应用此 IOCTL。 侦听连接请求的套接字必须申请此 IOCTL 接受连接。

一旦应用程序建立使用快速路径环回接口上的连接，连接的生存期内的所有数据包必须都使用快速路径。

将应用**SIO\_环回\_快速\_路径**到套接字将连接到非环回路径会产生任何效果。

此 TCP 环回优化会导致流通过传输层 (TL) 而不是传统环回通过网络层的数据包。 此优化可优化的环回数据包延迟。 连接级别设置，以使用环回快速路径的情况下，应用程序中选择，所有数据包将都按照环回路径。 对于环回通信，不应拥塞和数据包丢弃。 将不必要的拥塞控制和 TCP 中的可靠传递的概念。 但是，这不用于流控制，则返回 true。 没有流控制发件人会占用大量的接收缓冲区中，从而导致错误 TCP 环回行为。 TCP 优化的环回路径中的流控制由将发送请求置于队列中进行维护。 接收缓冲区已满时，TCP/IP 堆栈将保证发送队列已得到处理，维护流控制之前，不会完成。

出现的情况下连接数据的 Windows 筛选平台 (WFP) 标注 TCP 的快速路径环回连接必须执行的未优化的环回是慢速路径。 因此 WFP 筛选器将阻止从正在使用此新的环回快速路径。 启用 WFP 筛选器后，系统将使用慢速路径即使**SIO\_环回\_快速\_路径**IOCTL 已设置。 接下来就用户模式应用程序具有完整的 WFP 安全功能。

默认情况下**SIO\_环回\_快速\_路径**被禁用。

TCP/IP 套接字选项的一个子集是支持何时**SIO\_环回\_快速\_路径**IOCTL 用于启用对套接字的环回快速路径。 支持的选项的列表包括：

-   IP\_TTL
-   IP\_UNICAST\_IF
-   IPV6\_UNICAST\_HOPS
-   IPV6\_UNICAST\_IF
-   IPV6\_V6ONLY
-   [**SO\_CONDITIONAL\_ACCEPT**](https://docs.microsoft.com/windows/desktop/WinSock/so-conditional-accept)
-   [SO\_EXCLUSIVEADDRUSE](https://docs.microsoft.com/windows/desktop/WinSock/so-exclusiveaddruse)
-   [**因此\_端口\_可伸缩性**](https://docs.microsoft.com/windows/desktop/WinSock/so-port-scalability)
-   SO\_RCVBUF
-   因此\_REUSEADDR
-   TCP\_BSDURGENT

WSK 应用程序调用时必须指定一个指向 IRP 和完成例程[ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)对于此类型的请求的函数。 应用程序必须释放缓冲区，直到完成 IRP WSK 子系统。 完成后 IRP，子系统调用完成例程。 在完成例程中，应用程序必须检查 IRP 状态并释放它以前已分配给请求的所有资源。

有关 WSK IRP 处理的详细信息，请参阅[Winsock 内核函数使用 Irp](https://docs.microsoft.com/windows-hardware/drivers/network/using-irps-with-winsock-kernel-functions)。

完成后 IRP，将设置子系统*Irp-&gt;IoStatus.Status*到**状态\_成功**如果请求成功。 否则为*Irp-&gt;IoStatus.Status*将设置为**状态\_无效\_缓冲区\_大小**或**状态\_未\_支持**如果调用不成功。

## <a name="return-value"></a>返回值


<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 8</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Mstcpip.h</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**SIO\_LOOPBACK\_FAST\_PATH (SDK)** ](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/jj841212(v=vs.85))

[Irp 使用 Winsock 内核函数](https://docs.microsoft.com/windows-hardware/drivers/network/using-irps-with-winsock-kernel-functions)

 

 




