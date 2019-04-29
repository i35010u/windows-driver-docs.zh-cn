---
title: 包含 WDM 下边缘的微型端口驱动程序
description: 包含 WDM 下边缘的微型端口驱动程序
ms.assetid: e3acbcfe-b63d-441d-ab5f-26ee54a5d3ec
keywords:
- NDIS WDM 微型端口驱动程序 WDK 网络，有关 NDIS WDM 微型端口驱动程序
- NDIS WDM 微型端口驱动程序 WDK 网络组件
- NDIS 微型端口驱动程序 WDK 网络的下边缘
- WDM 较低的边缘 WDK 网络
- NDIS 微型端口驱动程序 WDK 网络，有关 WDM 下边缘的下边缘
- WDM 低边缘 WDK 网络，有关 WDM 下边缘
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e869d20fc9e72c5f870112e7c79312a7124ed68
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357270"
---
# <a name="miniport-driver-with-a-wdm-lower-edge"></a>包含 WDM 下边缘的微型端口驱动程序





使用 WDM 下边缘 （NDIS WDM 微型端口驱动程序） 的微型端口驱动程序遵循指定 WDM 标头文件，必须包含在驱动程序的源文件的 WDM 规则。 NDIS WDM 微型端口驱动程序需要在其下边缘上调用内核模式例程 WDM 标头文件。 通常情况下，NDIS 微型端口驱动程序应只调 NDIS 提供的函数。 此限制 NDIS 环绕的图中的 NDIS 微型端口驱动程序的方式显示[NDIS 驱动程序](ndis-drivers.md)部分。 虽然典型 NDIS 微型端口驱动程序不会调用 WDM 驱动程序，但它们间接地遵循了 WDM 规则，因为 NDIS 本身遵循 WDM 规则。

下图显示了使用 WDM 下边缘接口与 USB 驱动程序堆栈的 NDIS WDM 微型端口驱动程序。

![说明通过使用 wdm 下边缘接口与 usb 驱动程序堆栈的 ndis wdm 微型端口驱动程序的关系图](images/nonndslo.png)

以下列表介绍了上图显示的组件：

<a href="" id="ipx-spx-compatible-and-tcp-ip"></a>IPX/SPX 兼容和 TCP/IP  
[NDIS 协议驱动程序](ndis-protocol-drivers.md)的传输数据包通过使用基础的微型端口驱动程序。

<a href="" id="ndis"></a>NDIS  
提供了分层的网络驱动程序之间的标准接口 Ndis.sys 驱动程序。

<a href="" id="ndis-wdm-miniport-driver-for-usb"></a>有关 USB 的 NDIS WDM 微型端口驱动程序  
与 USB 驱动程序堆栈 NDIS WDM 微型端口驱动程序。

<a href="" id="usb-client-drivers"></a>USB 客户端驱动程序  
其他供应商提供 USB 客户端驱动程序。

<a href="" id="usb-class-interface"></a>USB 类接口  
[USB 例程](https://msdn.microsoft.com/library/windows/hardware/ff540046)并[I/O 请求](https://msdn.microsoft.com/library/windows/hardware/ff537421)，可以使用 USB 客户端驱动程序以便与 USB 驱动程序堆栈。

<a href="" id="usb-driver-stack"></a>USB 驱动程序堆栈  
USB 设备的驱动程序堆栈。 有关详细信息，请参阅[USB 驱动程序堆栈体系结构](https://msdn.microsoft.com/library/windows/hardware/hh406256)。

 

 





