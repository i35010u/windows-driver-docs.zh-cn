---
title: SIO_WSK_SET_TCP_SILENT_MODE 控制代码
description: SIO_WSK_SET_TCP_SILENT_MODE 套接字 i/o 控制操作允许 WSK 客户端启用 TCP 连接上的静默模式。
ms.assetid: 8ADC7FF4-86AC-4424-B763-8B62BF440D9F
ms.date: 07/18/2017
keywords:
- SIO_WSK_SET_TCP_SILENT_MODE 控制从 Windows Vista 开始的代码网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 834f248203b403a85776d04fdc6fab64db6d58cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841892"
---
# <a name="sio_wsk_set_tcp_silent_mode-control-code"></a>SIO\_WSK\_设置\_TCP\_缄默\_模式控制代码


**SIO\_WSK\_集\_tcp\_无提示\_模式**套接字 i/o 控制操作允许 WSK 客户端启用 TCP 连接上的静默模式。

在静默模式下，TCP 连接不会在网络上发送任何数据或控制数据包。 此套接字 i/o 控制操作仅适用于连接的 TCP 套接字。 它在环回时不受支持。

若要执行此操作，请调用具有以下参数的[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数。

<a name="parameters"></a>参数
----------

\[中的*RequestType*\]  
使用**WskIoctl**进行此操作。

\] 中的*ControlCode* \[  
操作的控制代码。 使用**SIO\_WSK\_将\_TCP\_为此操作设置为无提示\_模式**。

*级别*   
此操作使用零。

\] 中的*InputSize* \[  
此操作使用零。

\] 中的*InputBuffer* \[  
对于此操作，请使用**NULL** 。

*OutputSize* \[out\]  
此操作使用零。

\] 中的*OutputBuffer* \[  
对于此操作，请使用**NULL** 。

*OutputSizeReturned* \[out\]  
对于此操作，请使用**NULL** 。

<a name="remarks"></a>备注
-------

调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)函数以启用静默模式时，WSK 应用程序必须指定一个指向 IRP 的指针。

在调用[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)以启用静默模式之前，WSK 应用程序必须确保没有挂起的发送或断开连接请求。

启用静默模式时， [**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)将返回 **\_成功状态**。 一旦启用了静默模式，发送和断开连接请求将失败，**状态\_无效\_设备\_状态**，并且所有接收的控制或数据包将以静默方式丢弃。

此套接字上唯一有效的操作是[**WskCloseSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_close_socket)。

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
<td>Wsk （包括 Wsk）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**WskCloseSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_close_socket)

[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)

 

 




