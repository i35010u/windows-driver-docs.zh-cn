---
title: SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS 控制代码
description: SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS 套接字 I/O 控制操作允许 Winsock 客户端指定的重定向记录的新 TCP 套接字用于连接到最终目标。
ms.assetid: 51FC55BB-FD7A-4FDE-B1FC-02745AC03E33
ms.date: 08/08/2017
keywords: -SIO_SET_WFP_CONNECTION_REDIRECT_RECORDS 控制代码与 Windows Vista 一起启动的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: af3d7574c4be93ff65a9ba8596218f4274cabef5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379148"
---
# <a name="siosetwfpconnectionredirectrecords-control-code"></a>SIO\_设置\_WFP\_连接\_重定向\_记录控制代码


**SIO\_设置\_WFP\_连接\_重定向\_记录**套接字 I/O 控制操作允许 Winsock 客户端指定的重定向记录的新 TCP用于连接到最终目标的套接字。

WFP 重定向记录是不透明 WFP 必须对出站代理服务器的连接设置，以便重定向的连接，但逻辑上相关的原始连接的数据的缓冲区。

有关重定向的详细信息，请参阅[使用绑定或连接重定向](https://docs.microsoft.com/windows-hardware/drivers/network/using-bind-or-connect-redirection)。

若要设置为用于连接到最终目标的新 TCP 套接字的重定向记录，Winsock 客户端调用[ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)使用以下参数的函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>ReplTest1</th>
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
<td><p><em>Level</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>InputBuffer 参数指向的重定向记录的大小。</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>使用套接字关联的重定向记录指向的指针。</p></td>
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

 

Winsock 客户端必须分配缓冲区，并指定一个指向缓冲区和在其大小*InputBuffer*和*InputSize。*

Winsock 客户端调用时必须指定一个指向 IRP 和完成例程[ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)对于此类型的请求的函数。 客户端必须释放缓冲区，直到完成 IRP WSK 子系统。 完成后 IRP，子系统调用完成例程。 在完成例程中，客户端必须检查 IRP 状态并释放它以前已分配给请求的所有资源。

**请注意**  还有可能通过使用用户模式应用程序中执行此查询[ **SIO\_设置\_WFP\_连接\_重定向\_记录 (SDK)** ](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/hh859714(v=vs.85))。

 

有关 WSK IRP 处理的详细信息，请参阅[Winsock 内核函数使用 Irp](https://docs.microsoft.com/windows-hardware/drivers/network/using-irps-with-winsock-kernel-functions)。

客户端可以通过检查获取状态的 IRP *Irp-&gt;IoStatus.Status*。 *Irp-&gt;IoStatus.Status*将设置为**状态\_成功**如果请求成功。 否则，它将包含**状态\_整数\_OVERFLOW**，或**状态\_访问\_拒绝**如果调用不成功。

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

[**SIO\_设置\_WFP\_连接\_重定向\_记录 (SDK)** ](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/hh859714(v=vs.85))

 

 




