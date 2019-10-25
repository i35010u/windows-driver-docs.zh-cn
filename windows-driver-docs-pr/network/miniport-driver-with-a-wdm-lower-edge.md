---
title: 包含 WDM 下边缘的微型端口驱动程序
description: 包含 WDM 下边缘的微型端口驱动程序
ms.assetid: e3acbcfe-b63d-441d-ab5f-26ee54a5d3ec
keywords:
- NDIS-WDM 微型端口驱动程序 WDK 网络，关于 NDIS-WDM 微型端口驱动程序
- NDIS-WDM 微型端口驱动程序 WDK 网络，组件
- NDIS 微型端口驱动程序的下边缘 WDK 网络
- WDM 低边缘 WDK 网络
- NDIS 微型端口驱动程序的下边缘，WDK 网络，关于 WDM 下边缘
- WDM 低边缘 WDK 网络，关于 WDM 下边缘
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 356f2c2d33c0073f6a7c031d5ac026a598039e1c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844236"
---
# <a name="miniport-driver-with-a-wdm-lower-edge"></a>包含 WDM 下边缘的微型端口驱动程序





具有 WDM 下边缘的微型端口驱动程序（NDIS-WDM 微型端口驱动程序）遵循 WDM 规则，该规则指定 WDM 标头文件必须包含在驱动程序的源文件中。 NDIS-WDM 微型端口驱动程序要求使用 WDM 标头文件在其下边缘调用内核模式例程。 通常，NDIS 微型端口驱动程序应该只调用 NDIS 提供的函数。 此限制显示在 ndis[驱动](ndis-drivers.md)程序部分的图形中，NDIS 环绕 ndis 微型端口驱动程序的方式。 尽管典型的 NDIS 微型端口驱动程序不会被称为 WDM 驱动程序，但它们会间接遵循 WDM 规则，因为 NDIS 本身遵循 WDM 规则。

下图显示了通过使用 WDM 下边缘与 USB 驱动程序堆栈进行交互的 NDIS-WDM 微型端口驱动程序。

![说明通过使用 wdm 下边缘与 usb 驱动程序堆栈进行交互的 ndis wdm 微型端口驱动程序的示意图](images/nonndslo.png)

以下列表描述了上图中所示的组件：

<a href="" id="ipx-spx-compatible-and-tcp-ip"></a>IPX/SPX 兼容和 TCP/IP  
使用基础微型端口驱动程序传输数据包的[NDIS 协议驱动程序](ndis-protocol-drivers.md)。

<a href="" id="ndis"></a>以此  
在分层网络驱动程序之间提供标准接口的 Ndis .sys 驱动程序。

<a href="" id="ndis-wdm-miniport-driver-for-usb"></a>NDIS-适用于 USB 的 WDM 小型端口驱动程序  
与 USB 驱动程序堆栈交互的 NDIS-WDM 微型端口驱动程序。

<a href="" id="usb-client-drivers"></a>USB 客户端驱动程序  
其他供应商提供的 USB 客户端驱动程序。

<a href="" id="usb-class-interface"></a>USB 类接口  
Usb[例程](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85))和 i/o 请求，usb 客户端驱动程序可使用该[请求](https://docs.microsoft.com/previous-versions/ff537421(v=vs.85))与 usb 驱动程序堆栈进行交互。

<a href="" id="usb-driver-stack"></a>USB 驱动程序堆栈  
USB 设备的驱动程序堆栈。 有关详细信息，请参阅[USB 驱动程序堆栈体系结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

 

 





