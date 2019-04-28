---
title: 将 TDI 驱动程序移植到 Winsock 内核
description: 若要移植 TDI 驱动程序到 Winsock Kernel (WSK)，将需要将 TDI 任务转换为 WSK 的等效项，如下表中所示。
ms.assetid: 23662BF1-92EC-4C07-9A8D-F8F1D7D51692
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fbb55b0b9296abbad579ec82dd10d7bb622d7e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342979"
---
# <a name="porting-tdi-drivers-to-winsock-kernel"></a>将 TDI 驱动程序移植到 Winsock 内核


若要移植 TDI 驱动程序到 Winsock Kernel (WSK)，将需要将 TDI 任务转换为 WSK 的等效项，如下表中所示。

| 任务                            | TDI                                                                                       | Winsock 内核 (WSK)                                                                                                          |
|----------------------------------|-------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| 注册和取消注册          | 不可用                                                                                       | [**WskRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff571143)并[ **WskDeregister**](https://msdn.microsoft.com/library/windows/hardware/ff571128)                                       |
| 捕获和发布提供程序 NPI | 不可用                                                                                       | [**WskCaptureProviderNPI** ](https://msdn.microsoft.com/library/windows/hardware/ff571122)并[ **WskReleaseProviderNPI**](https://msdn.microsoft.com/library/windows/hardware/ff571145)   |
| 创建地址文件对象       | 创建*EaBuffer*，然后调用[ **zwcreatefile 转换**](https://msdn.microsoft.com/library/windows/hardware/ff566424)                      | 不再是必需的。 请参阅[ **WskSocket**](https://msdn.microsoft.com/library/windows/hardware/ff571149)。                                                                 |
| 创建连接文件对象    | 创建连接*EaBuffer*，然后调用[ **zwcreatefile 转换**](https://msdn.microsoft.com/library/windows/hardware/ff566424)           | 不再是必需的。 请参阅[ **WskSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571149)并[ *WskAcceptEvent*](https://msdn.microsoft.com/library/windows/hardware/ff571120)。                 |
| 将地址相关联                | [**TDI\_ASSOCIATE\_ADDRESS**](https://msdn.microsoft.com/library/windows/hardware/ff565080)                                | [**WskBind**](https://msdn.microsoft.com/library/windows/hardware/ff571121)                                                                                               |
| 设置事件处理程序               | [**TDI\_SET\_EVENT\_HANDLER**](https://msdn.microsoft.com/library/windows/hardware/ff565576)                               | [**WskControlSocket** ](https://msdn.microsoft.com/library/windows/hardware/ff571127)或使用静态的变体[ **WskControlClient**](https://msdn.microsoft.com/library/windows/hardware/ff571126) |
| 清除事件处理程序             | [**TDI\_SET\_EVENT\_HANDLER**](https://msdn.microsoft.com/library/windows/hardware/ff565576)                               | [**WskControlSocket**](https://msdn.microsoft.com/library/windows/hardware/ff571127)                                                                             |
| 连接                          | [**TDI\_CONNECT**](https://msdn.microsoft.com/library/windows/hardware/ff565083)                                                     | [**WskConnect**](https://msdn.microsoft.com/library/windows/hardware/ff571125)                                                                                         |
| 断开连接                       | [**TDI\_DISCONNECT**](https://msdn.microsoft.com/library/windows/hardware/ff565090)                                               | [**WskDisconnect**](https://msdn.microsoft.com/library/windows/hardware/ff571129)                                                                                   |
| Send                             | [**TDI\_SEND**](https://msdn.microsoft.com/library/windows/hardware/ff565549)                                                           | [**WskSend**](https://msdn.microsoft.com/library/windows/hardware/ff571146)                                                                                               |
| Receive                          | [**TDI\_RECEIVE**](https://msdn.microsoft.com/library/windows/hardware/ff565131)                                                     | [**WskReceive**](https://msdn.microsoft.com/library/windows/hardware/ff571139)                                                                                         |
| 取消关联地址             | [**TDI\_DISASSOCIATE\_ADDRESS**](https://msdn.microsoft.com/library/windows/hardware/ff565089)                          | 不可用                                                                                                                           |
| 接收处理程序                  | [**ClientEventReceive**](https://msdn.microsoft.com/library/windows/hardware/ff545260), [**TDI\_RECEIVE**](https://msdn.microsoft.com/library/windows/hardware/ff565131) | [*WskReceiveEvent*](https://msdn.microsoft.com/library/windows/hardware/ff571140)                                                                                 |
| 处理程序连接                  | [**ClientEventConnect**](https://msdn.microsoft.com/library/windows/hardware/ff544257)， [ **TDI\_连接**](https://msdn.microsoft.com/library/windows/hardware/ff565083) | [**WskAccept**](https://msdn.microsoft.com/library/windows/hardware/ff571109)                                                                                           |
| 关闭套接字或连接       | [**ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)或[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)    | [**WskCloseSocket**](https://msdn.microsoft.com/library/windows/hardware/ff571124)                                                                                 |

 

 

 





