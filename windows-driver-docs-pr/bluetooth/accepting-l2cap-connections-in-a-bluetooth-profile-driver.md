---
title: 在蓝牙配置文件驱动程序中接受 L2CAP 连接
description: 在蓝牙配置文件驱动程序中接受 L2CAP 连接
ms.assetid: 26a8238d-717a-438f-84d0-047ce9618928
keywords:
- L2CAP 配置文件驱动程序 WDK 蓝牙
- 逻辑链接控制器和适应协议 WDK 蓝牙
- 传入的 L2CAP 连接请求 WDK 蓝牙
- 连接 WDK 蓝牙
- 远程连接通知 WDK 蓝牙
- 通知 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 358c02116c2bbae1a35a543e0ef8a9f35fe816b9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328347"
---
# <a name="accepting-l2cap-connections-in-a-bluetooth-profile-driver"></a>在蓝牙配置文件驱动程序中接受 L2CAP 连接


L2CAP server 配置文件驱动程序对传入的逻辑链接控件和自适应协议 (L2CAP) 连接请求的响应从远程设备。 例如，PDA 的 L2CAP 服务器配置文件驱动程序将响应传入的连接请求从 PDA。

**若要接收传入 L2CAP 连接请求**

1.  **若要接收来自传入 L2CAP 连接请求*任何*远程设备的特定 PSM**，配置文件驱动程序应首先[生成并发送](building-and-sending-a-brb.md) [ **BRB\_L2CA\_注册\_服务器**](https://msdn.microsoft.com/library/windows/hardware/ff536618)请求，请指定**NULL**中**BtAddress**成员和中的为 0**Psm**的请求的成员\_BRB\_L2CA\_注册\_服务器结构。 配置文件驱动程序还必须注册[ *L2CAP 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536755)与蓝牙驱动程序堆栈在发送时**BRB\_L2CA\_注册\_SERVER**请求。 这样，要通知传入 L2CAP 连接请求的配置文件驱动程序的蓝牙驱动程序堆栈。

    然后，配置文件驱动程序应[生成并发送](building-and-sending-a-brb.md) [ **BRB\_注册\_PSM** ](https://msdn.microsoft.com/library/windows/hardware/ff536621)中请求，以便将接受蓝牙驱动程序堆栈从 PSM 注册请求的连接。 否则，蓝牙驱动程序堆栈会拒绝所有连接请求具有未知 （未注册） 的连接请求。 有关 PSMs 详细信息，请参阅[  **\_BRB\_PSM** ](https://msdn.microsoft.com/library/windows/hardware/ff536865)结构。

2.  **若要接收来自传入 L2CAP 连接请求*特定*远程设备/PSM 对**，配置文件驱动程序应[生成并发送](building-and-sending-a-brb.md) [ **BRB\_L2CA\_注册\_SERVER** ](https://msdn.microsoft.com/library/windows/hardware/ff536618)请求中，指定在远程设备的地址**BtAddress**成员，并在 PSM **Psm**成员的请求的随附\_BRB\_L2CA\_注册\_服务器结构。 配置文件驱动程序还必须注册[ *L2CAP 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536755)与蓝牙驱动程序堆栈在发送时**BRB\_L2CA\_注册\_SERVER**请求。 这样，要通知传入 L2CAP 连接请求的配置文件驱动程序的蓝牙驱动程序堆栈。

3.  配置文件驱动程序应发出[ **IOCTL\_同时为\_SDP\_提交\_记录**](https://msdn.microsoft.com/library/windows/hardware/ff536693)。 配置文件驱动程序然后可以注册一个 SDP 记录，其中介绍了配置文件驱动程序支持，该服务，以便远程系统可以通过使用 SDP 发现新的服务。

4.  蓝牙驱动程序堆栈时的蓝牙驱动程序堆栈从远程设备收到传入 L2CAP 连接请求，调用[ *L2CAP 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536755)以前注册配置文件驱动程序。 将值传递的蓝牙驱动程序堆栈**IndicationRemoteConnect**到*指示*回调函数的参数。

5.  若要响应传入的连接请求，配置文件驱动程序应[生成并发送](building-and-sending-a-brb.md) [ **BRB\_L2CA\_打开\_通道\_响应**](https://msdn.microsoft.com/library/windows/hardware/ff536616)请求。 服务器配置文件驱动程序将使用从蓝牙驱动程序堆栈传递的值*参数*要协商与远程设备的连接设置的回调函数的参数。 值的基础**响应**的成员[  **\_BRB\_L2CA\_打开\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff536860)结构与此请求一起传递，服务器配置文件驱动程序接受或拒绝连接请求。

6.  如果服务器配置文件驱动程序接受连接，然后可以调用蓝牙驱动程序堆栈[ *L2CAP 回调函数*](https://msdn.microsoft.com/library/windows/hardware/ff536755)中指定的那样**回调**的成员[  **\_BRB\_L2CA\_打开\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff536860)结构。 蓝牙驱动程序堆栈使用此函数来通知 L2CAP 连接的任何更改的服务器配置文件驱动程序。

**注意**  
-   单个配置文件驱动程序可以注册以接收来自多个传入 L2CAP 连接请求通过生成并发送多个不同的远程设备/PSM 对**BRB\_L2CA\_注册\_SERVER**请求，以注册多个 L2CAP 服务器，指定唯一的远程设备的地址和 PSM 中的对**BtAddress**并**Psm**成员的请求。

-   单个配置文件驱动程序可以注册以接收来自传入 L2CAP 连接请求*任何*远程设备的特定 PSM，以及接收传入 L2CAP 连接请求从多个不同的远程设备/PSM 对通过收到传入 L2CAP 连接请求来自任何远程设备的特定 PSM，第一个注册，并注册以接收传入 L2CAP 连接请求从特定的远程设备/PSM 配对，只要在中注册特定 PSM第一个步骤不会再注册。

-   多个配置文件驱动程序无法注册以收到传入 L2CAP 连接请求来自任何远程设备的相同 PSM。 蓝牙驱动程序堆栈仅允许一个配置文件驱动程序收到传入 L2CAP 连接请求来自任何远程设备的特定 PSM。

 

配置文件驱动程序接受连接请求后，它可以使用其他 BRBs 发送和接收数据，通过新建立的 L2CAP 连接。

若要停止接收通知的远程设备 L2CAP 连接尝试，配置文件驱动程序应[生成并发送](building-and-sending-a-brb.md) [ **BRB\_L2CA\_注销\_服务器**](https://msdn.microsoft.com/library/windows/hardware/ff536619)请求来取消注册服务器时配置文件驱动程序处理[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)插删除通知。

有关通知和回调函数的详细信息，请参阅[支持蓝牙事件通知](supporting-bluetooth-event-notifications.md)。

 

 





