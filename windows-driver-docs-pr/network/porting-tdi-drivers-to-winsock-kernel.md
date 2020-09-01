---
title: 将 TDI 驱动程序移植到 Winsock 内核
description: 若要将 TDI 驱动程序移植到 Winsock 内核 (WSK) ，需要将 TDI 任务转换为其 WSK 等效项，如下表所示。
ms.assetid: 23662BF1-92EC-4C07-9A8D-F8F1D7D51692
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c71251bff75bc4eb070e1b4b5c3a63d1409c1bdd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214500"
---
# <a name="porting-tdi-drivers-to-winsock-kernel"></a>将 TDI 驱动程序移植到 Winsock 内核


若要将 TDI 驱动程序移植到 Winsock 内核 (WSK) ，需要将 TDI 任务转换为其 WSK 等效项，如下表所示。

| 任务                            | TDI                                                                                       | Winsock 内核 (WSK)                                                                                                           |
|----------------------------------|-------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| 注册和取消注册          | 空值                                                                                       | [**WskRegister**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister)和[ **WskDeregister**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskderegister)                                       |
| 捕获和发布提供程序 NPI | 空值                                                                                       | [**WskCaptureProviderNPI**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi)和[ **WskReleaseProviderNPI**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskreleaseprovidernpi)   |
| 创建地址文件对象       | 创建 *EaBuffer*，然后调用 [**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)                      | 不再需要。 请参阅 [**WskSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)。                                                                 |
| 创建连接文件对象    | 创建连接 *EaBuffer*，然后调用 [**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)           | 不再需要。 请参阅 [**WskSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket) 和 [*WskAcceptEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event)。                 |
| 关联地址                | [**TDI \_ 关联 \_ 地址**](/previous-versions/windows/hardware/network/ff565080(v=vs.85))                                | [**WskBind**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_bind)                                                                                               |
| 设置事件处理程序               | [**TDI \_ 集 \_ 事件 \_ 处理程序**](/previous-versions/windows/hardware/network/ff565576(v=vs.85))                               | 使用 WskControlClient 的[**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)或静态变体[ **WskControlClient**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client) |
| 清除事件处理程序             | [**TDI \_ 集 \_ 事件 \_ 处理程序**](/previous-versions/windows/hardware/network/ff565576(v=vs.85))                               | [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)                                                                             |
| 连接                          | [**TDI \_ 连接**](/previous-versions/windows/hardware/network/ff565083(v=vs.85))                                                     | [**WskConnect**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_connect)                                                                                         |
| 断开连接                       | [**TDI \_ 断开连接**](/previous-versions/windows/hardware/network/ff565090(v=vs.85))                                               | [**WskDisconnect**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect)                                                                                   |
| 发送                             | [**TDI \_ 发送**](/previous-versions/windows/hardware/network/ff565549(v=vs.85))                                                           | [**WskSend**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send)                                                                                               |
| 接收                          | [**TDI \_ 接收**](/previous-versions/windows/hardware/network/ff565131(v=vs.85))                                                     | [**WskReceive**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive)                                                                                         |
| 解除地址关联             | [**TDI \_ 分离 \_ 地址**](/previous-versions/windows/hardware/network/ff565089(v=vs.85))                          | 空值                                                                                                                           |
| 接收处理程序                  | [**ClientEventReceive**](/previous-versions/windows/hardware/network/ff545260(v=vs.85))、 [ **TDI \_ 接收**](/previous-versions/windows/hardware/network/ff565131(v=vs.85)) | [*WskReceiveEvent*](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event)                                                                                 |
| 连接处理程序                  | [**ClientEventConnect**](/previous-versions/windows/hardware/network/ff544257(v=vs.85))、 [ **TDI \_ CONNECT**](/previous-versions/windows/hardware/network/ff565083(v=vs.85)) | [**WskAccept**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept)                                                                                           |
| 关闭套接字或连接       | [**ObDereferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)或[ **ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)    | [**WskCloseSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_close_socket)                                                                                 |

 

 

