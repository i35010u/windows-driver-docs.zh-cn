---
title: SIO_QUERY_WFP_CONNECTION_REDIRECT_RECORDS 控制代码
description: SIO_QUERY_WFP_CONNECTION_REDIRECT_RECORDS 套接字 i/o 控制操作允许 Winsock 客户端检索重定向连接的重定向记录。
ms.assetid: D04C63B8-DD08-4943-9F83-B5D05F4F2CCF
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SIO_QUERY_WFP_CONNECTION_REDIRECT_RECORDS 控制代码网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4b7dcd6d5a977c535623eb3881ab62c10987d277
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841905"
---
# <a name="sio_query_wfp_connection_redirect_records-control-code"></a>SIO\_QUERY\_WFP\_连接\_重定向\_记录控制代码


**SIO\_QUERY\_WFP\_连接\_重定向\_记录**套接字 i/o 控制操作允许 Winsock 客户端检索重定向连接的重定向记录。

WFP 重定向记录是不透明数据的缓冲区，WFP 必须在出站代理连接上设置，以便重定向的连接和原始连接在逻辑上是相关的。

**请注意**  **SIO\_QUERY\_wfp\_连接\_重定向\_** 仅当连接在 FWPS\_层重定向时才可使用\_**Ale\_连接\_\_V4**或**FWPS\_层\_ale\_\_V6**层由 WFP 客户端连接。\_

 

有关重定向的详细信息，请参阅[使用 Bind 或 Connect 重定向](https://docs.microsoft.com/windows-hardware/drivers/network/using-bind-or-connect-redirection)。

若要查询重定向连接的重定向记录，Winsock 客户端使用以下参数调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数。

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
<td><p><strong>SIO_QUERY_WFP_CONNECTION_REDIRECT_RECORDS</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>调配</em></p></td>
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
<td><p><em>OutputBuffer</em>参数指向的缓冲区的大小（以字节为单位）。</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向缓冲区的指针，该缓冲区接收已接受 TCP 连接的重定向记录。 缓冲区的大小在<em>OutputSize</em>参数中指定。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>指向<strong>ULONG</strong>类型的变量的指针，该变量接收复制到<em>OutputBuffer</em>参数指向的缓冲区中的数据字节数。</p></td>
</tr>
<tr class="odd">
<td><p>Irp</p></td>
<td><p>指向 IRP 的指针。</p></td>
</tr>
</tbody>
</table>

 

调用方可以通过以下两种方式之一执行此查询：

-   它可以将*OutputBuffer*设置为大小大约为 1 KB 的大缓冲区。 如果输出缓冲区大小不够大，则[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)将返回**状态\_缓冲区\_\_太小**并且*OutputSizeReturned*将包含所需的缓冲区大小。 然后，可以分配更大的缓冲区，并使用 SIO\_查询再次调用**WskControlSocket** **\_WFP\_连接\_将\_记录**请求和*OutputBuffer*设置为更大的缓冲区。
-   也可以将*OutputSize*参数设置为0，将*OUTPUTBUFFER*设置为 NULL，然后调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)。 完成后， **WskControlSocket**函数将检索*OutputSizeReturned*参数中的输出缓冲区大小（以字节为单位）。 然后，可以分配适当大小的缓冲区，并使用 SIO\_查询再次调用**WskControlSocket** **\_WFP\_连接\_重定向\_记录**请求，并将*OutputBuffer*设置为缓冲区。

**请注意**  在用户模式应用程序中，也可以使用[**SIO\_query\_WFP\_连接\_\_记录（SDK）** ](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/hh859713(v=vs.85))执行此查询。

 

对于这种类型的请求，Winsock 客户端必须指定一个指向 IRP 的指针以及一个指向其完成例程的指针。 IRP 可以通过更高的驱动程序传递给客户端，或者客户端可以选择分配 IRP。 若要指定完成例程，客户端必须调用[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)。 有关更多详细信息，请参阅将[irp 与 Winsock 内核函数配合使用](https://docs.microsoft.com/windows-hardware/drivers/network/using-irps-with-winsock-kernel-functions)。

在 WSK 子系统完成 IRP 之前，Winsock 客户端不能释放已分配的缓冲区。 WSK 子系统完成 IRP 后，它会通过调用完成例程通知客户端。 该缓冲区的引用通过完成例程的*上下文*参数中的 WSK 子系统传递给客户端。 缓冲区的大小存储在*Irp&gt;IoStatus*中。

客户端可以通过检查*irp-&gt;IoStatus*来获取 irp 的状态。 如果请求成功，则*Irp&gt;IoStatus*将设置为 " **\_状态**"。 否则，它将包含**状态\_整数\_溢出**、**状态\_\_未找到**、**状态\_缓冲区\_太小**，或**状态\_拒绝访问\_** 如果调用失败，则拒绝访问。\_

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

## <a name="see-also"></a>另请参阅


[使用 Bind 或 Connect 重定向](https://docs.microsoft.com/windows-hardware/drivers/network/using-bind-or-connect-redirection)

[将 Irp 与 Winsock 内核函数结合使用](https://docs.microsoft.com/windows-hardware/drivers/network/using-irps-with-winsock-kernel-functions)

[**SIO\_QUERY\_WFP\_连接\_重定向\_上下文**](sio-query-wfp-connection-redirect-context.md)

[**SIO\_QUERY\_WFP\_连接\_重定向\_记录（SDK）** ](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/hh859713(v=vs.85))

[**SIO\_设置\_WFP\_连接\_重定向\_记录**](sio-set-wfp-connection-redirect-records.md)

 

 




