---
title: SIO_WSK_SET_TCP_SILENT_MODE 控制代码
description: SIO_WSK_SET_TCP_SILENT_MODE 套接字 i/o 控制操作允许 WSK 客户端启用 TCP 连接上的静默模式。
ms.assetid: 8ADC7FF4-86AC-4424-B763-8B62BF440D9F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 SIO_WSK_SET_TCP_SILENT_MODE 控制代码网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c5b698f03e0b8f360c013e166540b20afe9f2076
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216584"
---
# <a name="sio_wsk_set_tcp_silent_mode-control-code"></a>SIO \_ WSK \_ 设置 \_ TCP \_ 静默 \_ 模式控制代码


**SIO \_ WSK \_ 设置 \_ tcp \_ 静默 \_ 模式**套接字 i/o 控制操作允许 WSK 客户端启用 TCP 连接上的静默模式。

在静默模式下，TCP 连接不会在网络上发送任何数据或控制数据包。 此套接字 i/o 控制操作仅适用于连接的 TCP 套接字。 它在环回时不受支持。

若要执行此操作，请调用具有以下参数的 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数。

<a name="parameters"></a>参数
----------

*RequestType* \[中\]  
使用 **WskIoctl** 进行此操作。

*ControlCode* \[中\]  
操作的控制代码。 对于此操作，请使用 **SIO \_ WSK \_ 设置 \_ TCP \_ 静默 \_ 模式** 。

*调配*   
此操作使用零。

*InputSize* \[中\]  
此操作使用零。

*InputBuffer* \[中\]  
对于此操作，请使用 **NULL** 。

*OutputSize* \[弄\]  
此操作使用零。

*OutputBuffer* \[中\]  
对于此操作，请使用 **NULL** 。

*OutputSizeReturned* \[弄\]  
对于此操作，请使用 **NULL** 。

<a name="remarks"></a>备注
-------

调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数以启用静默模式时，WSK 应用程序必须指定一个指向 IRP 的指针。

在调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 以启用静默模式之前，WSK 应用程序必须确保没有挂起的发送或断开连接请求。

启用静默模式时， [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)将返回**状态 " \_ 成功**"。 一旦启用了静默模式，发送和断开连接的请求将失败，并且状态为 " ** \_ \_ 设备 \_ 状态无效** "，所有接收的控件或数据包将以静默方式丢弃。

此套接字上唯一有效的操作是 [**WskCloseSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_close_socket)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows 8、Windows Server 2012 和更高版本中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wsk (包含 Wsk) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WskCloseSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_close_socket)

[**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)

 

