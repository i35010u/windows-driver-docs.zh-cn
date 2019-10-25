---
title: SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS 控制代码
description: SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS 套接字 i/o 控制操作允许 Winsock 客户端指定用于连接到最终目标的新 TCP 套接字的重定向记录。
ms.assetid: 51FC55BB-FD7A-4FDE-B1FC-02745AC03E33
ms.date: 08/08/2017
keywords: -SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS 控制从 Windows Vista 开始的代码网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b3617d012cff3a28638a0c8991ba039b5c3f7a14
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841907"
---
# <a name="sio_set_wfp_connection_redirect_records-control-code"></a>SIO\_设置\_WFP\_连接\_重定向\_记录控制代码


**SIO\_设置\_WFP\_连接\_重定向\_记录**套接字 i/o 控制操作允许 Winsock 客户端指定用于连接到最终目标的新 TCP 套接字的重定向记录。

WFP 重定向记录是不透明数据的缓冲区，WFP 必须在出站代理连接上设置，以便重定向的连接和原始连接在逻辑上是相关的。

有关重定向的详细信息，请参阅[使用 Bind 或 Connect 重定向](https://docs.microsoft.com/windows-hardware/drivers/network/using-bind-or-connect-redirection)。

若要将重定向记录设置为用于连接到最终目标的新 TCP 套接字，Winsock 客户端使用以下参数调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>Value</th>
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
<td><p><em>调配</em></p></td>
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
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="odd">
<td><p>Irp</p></td>
<td><p>指向 IRP 的指针。</p></td>
</tr>
</tbody>
</table>

 

Winsock 客户端必须分配一个缓冲区，并在*InputBuffer*和 InputSize 中指定一个指向缓冲区的指针及其大小 *。*

在调用此类型的请求的[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数时，Winsock 客户端必须指定指向 IRP 和完成例程的指针。 在 WSK 子系统完成 IRP 之前，客户端不能释放缓冲区。 完成 IRP 后，子系统将调用完成例程。 在完成例程中，客户端必须检查 IRP 状态，并释放以前为请求分配的所有资源。

**请注意**  在用户模式应用程序中，也可以使用[**SIO\_设置\_WFP\_连接\_\_记录（SDK）** ](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/hh859714(v=vs.85))，在用户模式应用程序中执行此查询。

 

有关 WSK IRP 处理的详细信息，请参阅将[irp 与 Winsock 内核函数配合使用](https://docs.microsoft.com/windows-hardware/drivers/network/using-irps-with-winsock-kernel-functions)。

客户端可以通过检查*irp-&gt;IoStatus*来获取 irp 的状态。 如果请求成功，则*Irp&gt;IoStatus*将设置为 " **\_状态**"。 否则，如果调用不成功，它将包含 **\_整数\_溢出**或**状态\_拒绝\_访问**的状态。

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

[**SIO\_QUERY\_WFP\_连接\_重定向\_记录**](sio-query-wfp-connection-redirect-records.md)

[**SIO\_设置\_WFP\_连接\_重定向\_记录（SDK）** ](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/hh859714(v=vs.85))

 

 




