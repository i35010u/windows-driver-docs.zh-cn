---
title: SIO_WSK_SET_TCP_SILENT_MODE 控制代码
description: SIO_WSK_SET_TCP_SILENT_MODE 套接字 I/O 控制操作允许 WSK 客户端启用的 TCP 连接上的无提示模式。
ms.assetid: 8ADC7FF4-86AC-4424-B763-8B62BF440D9F
ms.date: 07/18/2017
keywords:
- SIO_WSK_SET_TCP_SILENT_MODE 控制代码与 Windows Vista 一起启动的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8015a45c335ccd797f0edeb4fe5aba4e49c362a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376417"
---
# <a name="siowsksettcpsilentmode-control-code"></a>SIO\_WSK\_设置\_TCP\_无提示\_模式控制代码


**SIO\_WSK\_设置\_TCP\_无提示\_模式**套接字 I/O 控制操作允许 WSK 客户端启用的 TCP 连接上的无提示模式。

在静默模式下的 TCP 连接不会在网络上发送任何数据或控制数据包。 此套接字的 I/O 控制操作仅适用于已连接的 TCP 套接字。 它不支持环回。

若要执行此操作，调用[ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)使用以下参数的函数。

<a name="parameters"></a>Parameters
----------

*RequestType* \[中\]  
使用**WskIoctl**对于此操作。

*ControlCode* \[in\]  
操作的控制代码。 使用**SIO\_WSK\_设置\_TCP\_无提示\_模式**对于此操作。

*级别*   
此操作，则使用零。

*InputSize* \[in\]  
此操作，则使用零。

*InputBuffer* \[in\]  
使用**NULL**对于此操作。

*OutputSize* \[out\]  
此操作，则使用零。

*OutputBuffer* \[in\]  
使用**NULL**对于此操作。

*OutputSizeReturned* \[out\]  
使用**NULL**对于此操作。

<a name="remarks"></a>备注
-------

WSK 应用程序调用时必须指定一个指向 IRP [ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)函数可启用无提示模式。

WSK 应用程序之前调用[ **WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)若要启用无提示模式下必须确保没有任何挂起的发送或断开连接请求。

[**WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)将返回**状态\_成功**启用无提示模式下时。 一旦启用了无提示模式下，发送和断开的连接请求将失败，**状态\_无效\_设备\_状态**，将以无提示方式忽略所有接收到的控件或数据数据包。

此套接字上的唯一有效操作是[ **WskCloseSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_close_socket)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows 8，Windows Server 2012，及更高版本中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wsk.h （包括 Wsk.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WskCloseSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_close_socket)

[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)

 

 




