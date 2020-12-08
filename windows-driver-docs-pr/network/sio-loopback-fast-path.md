---
title: SIO_LOOPBACK_FAST_PATH 控制代码
description: SIO_LOOPBACK_FAST_PATH 套接字 i/o 控制代码允许 WSK 应用程序配置 TCP 套接字，以便更快地在环回接口上操作。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SIO_LOOPBACK_FAST_PATH 控制代码网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1f4b8e69bbe8b6738cd00e1c02233578c650aa8d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837663"
---
# <a name="sio_loopback_fast_path-control-code"></a>SIO \_ 环回 \_ 快速 \_ 路径控制代码


**重要提示** **SIO \_ 环回 \_ FAST \_ 路径** 已弃用，不建议在代码中使用。

 

**SIO \_ 环回 \_ FAST \_ PATH** 套接字 i/o 控制代码允许 WSK 应用程序配置 TCP 套接字，以便更快地在环回接口上操作。

若要使用此 IOCTL，WSK 应用程序需要使用以下参数调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>“值”</th>
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
<td><p><em>级别</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>输入缓冲区的大小（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向输入缓冲区的指针。 此参数包含一个指向布尔值的指针，该 <strong>布尔</strong> 值指示是否应为快速环回操作配置套接字。</p></td>
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

 

应用程序可以使用 **SIO \_ 环回 \_ FAST \_ 路径** IOCTL 提高 TCP 套接字上环回操作的性能。 此 IOCTL 请求 TCP/IP 堆栈为此套接字上的环回操作使用特殊的快速路径。 **SIO \_ 环回 \_ FAST \_ 路径** IOCTL 只能与 TCP 套接字一起使用。 此 IOCTL 必须在环回会话两侧使用。 使用 IPv4 或 IPv6 环回接口支持 TCP 环回快速路径。

计划启动连接请求的套接字必须应用此 IOCTL，才能发出连接请求。 侦听连接请求的套接字必须应用此 IOCTL 才能接受连接。

当应用程序使用 fast 路径在环回接口上建立连接后，该连接的生存期的所有数据包都必须使用快速路径。

将 **SIO \_ 环回 \_ FAST \_ 路径** 应用到将连接到非回送路径的套接字将不起作用。

此 TCP 环回优化导致数据包通过传输层 (TL) 而不是通过网络层进行传统环回。 此优化可缩短环回数据包的延迟时间。 一旦某个应用程序将连接级别设置为使用环回快速路径，所有数据包就会按照环回路径进行。 对于环回通信，不需要拥塞和数据包丢弃。 TCP 中的拥塞控制和可靠传递的概念是不必要的。 不过，对于流控制，这种情况并不适用。 如果没有 flow 控制，发送方可能会严重影响接收缓冲区，从而导致 TCP 环回行为错误。 通过在队列中放置发送请求，维护 TCP 优化环回路径中的流控制。 当接收缓冲区已满时，TCP/IP 堆栈保证发送完成后才会完成，直到处理队列，维护流控制。

存在 Windows 筛选平台时的 TCP 快速路径环回连接 (WFP) callout 连接数据必须采用未优化的慢速路径进行环回。 因此，WFP 筛选器将阻止使用此新的环回快速路径。 启用 WFP 筛选器后，即使设置了 **SIO \_ 环回 \_ FAST \_ 路径** IOCTL，系统也会使用慢速路径。 这可以了用户模式应用程序具有完整的 WFP 安全功能。

默认情况下， **SIO \_ 环回 \_ FAST \_ PATH** 处于禁用状态。

当使用 **SIO \_ 环回 \_ 快速 \_ 路径** IOCTL 在套接字上启用环回快速路径时，仅支持 tcp/ip 套接字选项的子集。 支持的选项列表包括以下各项：

-   IP \_ TTL
-   IP \_ 单播 \_ IF
-   IPV6 \_ 单播 \_ 跃点
-   IPV6 \_ 单播 \_ IF
-   IPV6 \_ V6ONLY
-   [**SO \_ 条件 \_ 接受**](/windows/desktop/WinSock/so-conditional-accept)
-   [\_EXCLUSIVEADDRUSE](/windows/desktop/WinSock/so-exclusiveaddruse)
-   [**如此 \_ 端口的 \_ 可伸缩性**](/windows/desktop/WinSock/so-port-scalability)
-   \_RCVBUF
-   \_REUSEADDR
-   TCP \_ BSDURGENT

为此类型的请求调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数时，WSK 应用程序必须指定指向 IRP 和完成例程的指针。 在 WSK 子系统完成 IRP 之前，应用程序不能释放缓冲区。 完成 IRP 后，子系统将调用完成例程。 在完成例程中，应用程序必须检查 IRP 状态，并释放以前为请求分配的所有资源。

有关 WSK IRP 处理的详细信息，请参阅将 [irp 与 Winsock 内核函数配合使用](./using-irps-with-winsock-kernel-functions.md)。

完成 IRP 后，如果请求成功，子系统会将 *IRP &gt; IoStatus* 设置为 **状态 " \_ 成功** "。 否则， *&gt; IoStatus* 将设置为 " **状态 \_ 无效 \_ 缓冲区 \_ 大小** " 或在调用不成功时 **\_ 不 \_ 支持的状态** 。

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
<td><p>标头</p></td>
<td>Mstcpip.h</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**SIO \_ 环回 \_ FAST \_ 路径 (SDK)**](/windows/win32/winsock/sio-loopback-fast-path)

[将 IRP 与 Winsock 内核函数配合使用](./using-irps-with-winsock-kernel-functions.md)

 

