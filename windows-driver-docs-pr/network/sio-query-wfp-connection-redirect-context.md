---
title: SIO_QUERY_WFP_CONNECTION_REDIRECT_CONTEXT 控制代码
description: SIO_QUERY_WFP_CONNECTION_REDIRECT_CONTEXT 套接字 I/O 控制操作允许 Winsock 客户端检索重定向的连接的重定向记录的重定向上下文。
ms.assetid: D23971FC-D75F-4C39-BE6A-F0E17F7C1804
ms.date: 08/08/2017
keywords: -SIO_QUERY_WFP_CONNECTION_REDIRECT_CONTEXT 控制代码与 Windows Vista 一起启动的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6cc4bbc74ea66735950224151eb321ee64e1fbc9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379159"
---
# <a name="sioquerywfpconnectionredirectcontext-control-code"></a>SIO\_查询\_WFP\_连接\_重定向\_上下文控制代码


**SIO\_查询\_WFP\_连接\_重定向\_上下文**套接字 I/O 控制操作允许 Winsock 客户端检索的重定向上下文重定向的重定向连接的记录。

WFP 重定向记录是不透明 WFP 必须对出站代理服务器的连接设置，以便重定向的连接，但逻辑上相关的原始连接的数据的缓冲区。

**请注意**   [ **SIO\_查询\_WFP\_连接\_重定向\_记录**](sio-query-wfp-connection-redirect-records.md)查询可以如果连接已重定向在仅使用**FWPS\_层\_ALE\_CONNECT\_重定向\_V4**或**FWPS\_层\_ALE\_CONNECT\_重定向\_V6** WFP 客户端层。

 

有关重定向的详细信息，请参阅[使用绑定或连接重定向](https://docs.microsoft.com/windows-hardware/drivers/network/using-bind-or-connect-redirection)。

若要查询重定向记录的重定向上下文，Winsock 客户端调用[ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)使用以下参数的函数。

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
<td><p><strong>SIO_QUERY_WFP_CONNECTION_REDIRECT_CONTEXT</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>Level</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>大小 （字节） 所指向的缓冲区<em>OutputBuffer</em>参数。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向接收重定向上下文接受 TCP 连接的重定向记录的缓冲区的指针。 中指定的缓冲区的大小<em>OutputSize</em>参数。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>一个指向<strong>ULONG</strong>-接收的数据复制到所指向的缓冲区的字节数的类型化的变量<em>OutputBuffer</em>参数。</p></td>
</tr>
<tr class="odd">
<td><p>Irp</p></td>
<td><p>指向 IRP 的指针。</p></td>
</tr>
</tbody>
</table>

 

调用方可以通过以下方式之一执行此查询：

-   可以设置*OutputBuffer*到大型缓冲区的大小大约为 1 KB。 如果输出缓冲区大小不足够，大[ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)将返回**状态\_缓冲区\_过\_小**和*OutputSizeReturned*将包含所需的缓冲区大小。 然后可以分配较大的缓冲区并**WskControlSocket**再次调用**SIO\_查询\_WFP\_连接\_重定向\_上下文**请求和*OutputBuffer*设置为更大的缓冲区。
-   也可以设置*OutputSize*为 0 的参数和*OutputBuffer*为 NULL，且然后调用[ **WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)。 完成后， **WskControlSocket**函数中检索输出缓冲区大小，以字节为单位， *OutputSizeReturned*参数。 然后可以分配相应大小的缓冲区并**WskControlSocket**再次调用**SIO\_查询\_WFP\_连接\_重定向\_上下文**请求并*OutputBuffer*设置到缓冲区。

**请注意**  还有可能通过使用用户模式应用程序中执行此查询[ **SIO\_查询\_WFP\_连接\_重定向\_上下文 (SDK)** ](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/hh859712(v=vs.85))。

 

对于此类型的请求，Winsock 客户端必须指定指向 IRP 的指针和指向其完成例程的指针。 更高版本的驱动程序，可以将 IRP 传递给客户端或客户端可以选择分配 IRP。 若要指定完成例程，客户端必须调用[ **IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)。 有关更多详细信息，请参阅[Winsock 内核函数使用 Irp](https://docs.microsoft.com/windows-hardware/drivers/network/using-irps-with-winsock-kernel-functions)。

Winsock 客户端必须释放分配的缓冲区，直到 IRP 完成 WSK 子系统。 WSK 子系统完成 IRP，它将通知客户端通过调用完成例程。 中的 WSK 子系统对该缓冲区的引用传递给客户端*上下文*完成例程的参数。 缓冲区的大小存储在*Irp-&gt;IoStatus.Information*。

客户端可以通过检查获取状态的 IRP *Irp-&gt;IoStatus.Status*。 *Irp-&gt;IoStatus.Status*将设置为**状态\_成功**如果请求成功。 否则，它将包含**状态\_整数\_OVERFLOW**，**状态\_不\_找到**，**状态\_缓冲区\_过\_小**，或**状态\_访问\_拒绝**如果调用不成功。

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


[使用绑定或连接重定向](https://docs.microsoft.com/windows-hardware/drivers/network/using-bind-or-connect-redirection)

[Irp 使用 Winsock 内核函数](https://docs.microsoft.com/windows-hardware/drivers/network/using-irps-with-winsock-kernel-functions)

[**SIO\_查询\_WFP\_连接\_重定向\_记录**](sio-query-wfp-connection-redirect-records.md)

[**SIO\_查询\_WFP\_连接\_重定向\_上下文 (SDK)** ](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/hh859712(v=vs.85))

 

 




