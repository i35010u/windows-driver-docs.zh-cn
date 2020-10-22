---
title: SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS 控制代码
description: SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS 套接字 i/o 控制操作允许 Winsock 客户端指定重定向记录到用于连接到最终目标的新 TCP 套接字。
ms.assetid: 51FC55BB-FD7A-4FDE-B1FC-02745AC03E33
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS 控制代码网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ed11e8b3082c04e5ab09e8d440638d1691b7acdb
ms.sourcegitcommit: a866b3470025d85b25a48857a81f893179698e7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92356003"
---
# <a name="sio_set_wfp_connection_redirect_records-control-code"></a>SIO \_ SET \_ WFP \_ 连接 \_ 重定向 \_ 记录控制代码


**SIO \_ SET \_ WFP \_ 连接 \_ 重定向 \_ 记录**套接字 i/o 控制操作允许 Winsock 客户端指定用于连接到最终目标的新 TCP 套接字的重定向记录。

WFP 重定向记录是不透明数据的缓冲区，WFP 必须在出站代理连接上设置，以便重定向的连接和原始连接在逻辑上是相关的。

有关重定向的详细信息，请参阅 [使用 Bind 或 Connect 重定向](./using-bind-or-connect-redirection.md)。

若要将重定向记录设置为用于连接到最终目标的新 TCP 套接字，Winsock 客户端使用以下参数调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数。

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
<td><p><strong>SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS</strong></p></td>
</tr>
<tr class="odd">
<td><p><em>级别</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>InputBuffer 参数指向的重定向记录的大小。</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向与套接字关联的重定向记录的指针。</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>Null</p></td>
</tr>
<tr class="odd">
<td><p>Irp</p></td>
<td><p>指向 IRP 的指针。</p></td>
</tr>
</tbody>
</table>

 

Winsock 客户端必须分配一个缓冲区，并在 *InputBuffer* 和 InputSize 中指定一个指向缓冲区的指针及其大小 *。*

在调用此类型的请求的 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数时，Winsock 客户端必须指定指向 IRP 和完成例程的指针。 在 WSK 子系统完成 IRP 之前，客户端不能释放缓冲区。 完成 IRP 后，子系统将调用完成例程。 在完成例程中，客户端必须检查 IRP 状态，并释放以前为请求分配的所有资源。

**注意**  还可以使用 [**SIO \_ SET \_ WFP \_ 连接 \_ 重定向 \_ 记录 (SDK) **](/windows/win32/winsock/sio-set-wfp-connection-redirect-records)在用户模式应用程序中执行此查询。

 

有关 WSK IRP 处理的详细信息，请参阅将 [irp 与 Winsock 内核函数配合使用](./using-irps-with-winsock-kernel-functions.md)。

客户端可以通过检查 *irp- &gt; IOSTATUS*获取 irp 的状态。 *Irp- &gt;* 如果请求成功，则将 IoStatus 状态设置为 " ** \_ 成功**"。 否则，它将包含 **状态 \_ 整数 \_ 溢出**，或在调用不成功时 ** \_ \_ 拒绝访问状态** 。

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

## <a name="see-also"></a>另请参阅


[使用绑定或连接重定向](./using-bind-or-connect-redirection.md)

[将 IRP 与 Winsock 内核函数配合使用](./using-irps-with-winsock-kernel-functions.md)

[**SIO \_ 查询 \_ WFP \_ 连接 \_ 重定向 \_ 记录**](sio-query-wfp-connection-redirect-records.md)

[**SIO \_ SET \_ WFP \_ 连接 \_ 重定向 \_ 记录 (SDK) **](/windows/win32/winsock/sio-set-wfp-connection-redirect-records)

 

