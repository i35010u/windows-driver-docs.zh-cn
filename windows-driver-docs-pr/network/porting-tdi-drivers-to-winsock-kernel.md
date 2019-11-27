---
title: 将 TDI 驱动程序移植到 Winsock 内核
description: 若要将 TDI 驱动程序移植到 Winsock 内核（WSK），需要将 TDI 任务转换为其 WSK 等效项，如下表所示。
ms.assetid: 23662BF1-92EC-4C07-9A8D-F8F1D7D51692
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 684af6ea6ad39663ccd12f481ffe1ea180f03a40
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843685"
---
# <a name="porting-tdi-drivers-to-winsock-kernel"></a>将 TDI 驱动程序移植到 Winsock 内核


若要将 TDI 驱动程序移植到 Winsock 内核（WSK），需要将 TDI 任务转换为其 WSK 等效项，如下表所示。

| 任务                            | TDI                                                                                       | Winsock 内核（WSK）                                                                                                          |
|----------------------------------|-------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| 注册和取消注册          | N/A                                                                                       | [**WskRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister)和[ **WskDeregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskderegister)                                       |
| 捕获和发布提供程序 NPI | N/A                                                                                       | [**WskCaptureProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi)和[ **WskReleaseProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskreleaseprovidernpi)   |
| 创建地址文件对象       | 创建*EaBuffer*，然后调用[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)                      | 不再需要。 请参阅[**WskSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)。                                                                 |
| 创建连接文件对象    | 创建连接*EaBuffer*，然后调用[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)           | 不再需要。 请参阅[**WskSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)和[*WskAcceptEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept_event)。                 |
| 关联地址                | [**TDI\_关联\_地址**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565080(v=vs.85))                                | [**WskBind**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_bind)                                                                                               |
| 设置事件处理程序               | [**TDI\_设置\_事件\_处理程序**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565576(v=vs.85))                               | 使用 WskControlClient 的[**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)或静态变体[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client) |
| 清除事件处理程序             | [**TDI\_设置\_事件\_处理程序**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565576(v=vs.85))                               | [**WskControlSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket)                                                                             |
| 连接                          | [**TDI\_连接**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565083(v=vs.85))                                                     | [**WskConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_connect)                                                                                         |
| 断开连接                       | [**TDI\_断开连接**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565090(v=vs.85))                                               | [**WskDisconnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_disconnect)                                                                                   |
| 发送                             | [**TDI\_发送**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565549(v=vs.85))                                                           | [**WskSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send)                                                                                               |
| Receive                          | [**TDI\_接收**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565131(v=vs.85))                                                     | [**WskReceive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive)                                                                                         |
| 解除地址关联             | [**TDI\_解除\_地址的关联**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565089(v=vs.85))                          | N/A                                                                                                                           |
| 接收处理程序                  | [**ClientEventReceive**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545260(v=vs.85))、 [ **TDI\_接收**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565131(v=vs.85)) | [*WskReceiveEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event)                                                                                 |
| 连接处理程序                  | [**ClientEventConnect**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff544257(v=vs.85))、 [ **TDI\_连接**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565083(v=vs.85)) | [**WskAccept**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_accept)                                                                                           |
| 关闭套接字或连接       | [**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)或[ **ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)    | [**WskCloseSocket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_close_socket)                                                                                 |

 

 

 





