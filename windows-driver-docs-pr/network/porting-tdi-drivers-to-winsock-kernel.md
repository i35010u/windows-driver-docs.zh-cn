---
title: 将 TDI 驱动程序移植到 Winsock 内核
description: 若要移植 TDI 驱动程序到 Winsock Kernel (WSK)，将需要将 TDI 任务转换为 WSK 的等效项，如下表中所示。
ms.assetid: 23662BF1-92EC-4C07-9A8D-F8F1D7D51692
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f08c14e568f1f2c2399de4ca3127e2d30233709
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384536"
---
# <a name="porting-tdi-drivers-to-winsock-kernel"></a>将 TDI 驱动程序移植到 Winsock 内核


若要移植 TDI 驱动程序到 Winsock Kernel (WSK)，将需要将 TDI 任务转换为 WSK 的等效项，如下表中所示。

| 任务                            | TDI                                                                                       | Winsock 内核 (WSK)                                                                                                          |
|----------------------------------|-------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| 注册和取消注册          | 不可用                                                                                       | [**WskRegister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskregister)并[ **WskDeregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskderegister)                                       |
| 捕获和发布提供程序 NPI | 不可用                                                                                       | [**WskCaptureProviderNPI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskcaptureprovidernpi)并[ **WskReleaseProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskreleaseprovidernpi)   |
| 创建地址文件对象       | 创建*EaBuffer*，然后调用[ **zwcreatefile 转换**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)                      | 不再是必需的。 请参阅[ **WskSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket)。                                                                 |
| 创建连接文件对象    | 创建连接*EaBuffer*，然后调用[ **zwcreatefile 转换**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)           | 不再是必需的。 请参阅[ **WskSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_socket)并[ *WskAcceptEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_accept_event)。                 |
| 将地址相关联                | [**TDI\_ASSOCIATE\_ADDRESS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565080(v=vs.85))                                | [**WskBind**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_bind)                                                                                               |
| 设置事件处理程序               | [**TDI\_SET\_EVENT\_HANDLER**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565576(v=vs.85))                               | [**WskControlSocket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)或使用静态的变体[ **WskControlClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_client) |
| 清除事件处理程序             | [**TDI\_SET\_EVENT\_HANDLER**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565576(v=vs.85))                               | [**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_control_socket)                                                                             |
| 连接                          | [**TDI\_CONNECT**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565083(v=vs.85))                                                     | [**WskConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_connect)                                                                                         |
| 断开连接                       | [**TDI\_DISCONNECT**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565090(v=vs.85))                                               | [**WskDisconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_disconnect)                                                                                   |
| Send                             | [**TDI\_SEND**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565549(v=vs.85))                                                           | [**WskSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_send)                                                                                               |
| Receive                          | [**TDI\_RECEIVE**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565131(v=vs.85))                                                     | [**WskReceive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive)                                                                                         |
| 取消关联地址             | [**TDI\_DISASSOCIATE\_ADDRESS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565089(v=vs.85))                          | 不可用                                                                                                                           |
| 接收处理程序                  | [**ClientEventReceive**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545260(v=vs.85)), [**TDI\_RECEIVE**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565131(v=vs.85)) | [*WskReceiveEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_receive_event)                                                                                 |
| 处理程序连接                  | [**ClientEventConnect**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff544257(v=vs.85))， [ **TDI\_连接**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565083(v=vs.85)) | [**WskAccept**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_accept)                                                                                           |
| 关闭套接字或连接       | [**ObDereferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)或[ **ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)    | [**WskCloseSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nc-wsk-pfn_wsk_close_socket)                                                                                 |

 

 

 





