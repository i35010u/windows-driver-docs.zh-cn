---
title: WDM 低接口概述的小型端口驱动程序
description: WDM 低接口概述的小型端口驱动程序
ms.assetid: defa955b-c1d2-4c78-a983-584aedc8a1a3
keywords:
- 微型端口驱动程序 WDK 网络, WDM 低端接口
- NDIS 微型端口驱动程序 WDK, WDM 低端接口
- NDIS-WDM 微型端口驱动程序 WDK 网络
- WDM 低端接口 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5955984828ef998a0354e0b318cc770a5af6235e
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565143"
---
# <a name="overview-of-miniport-drivers-with-a-wdm-lower-interface"></a>WDM 低接口概述的小型端口驱动程序





带有 Microsoft [Windows 驱动模型](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)(WDM) 较低接口的小型小型驱动程序也称为*NDIS-WDM 微型端口驱动程序*。 这种类型的微型端口驱动程序:

-   使用 WDM 下边缘。

-   可以调用 NDIS 和非 NDIS 函数。 但是, 如果有可能, 微型端口驱动程序应调用 NDIS 函数。

-   可以初始化微型端口实例, 该实例用于控制连接到特定总线并通过该总线与这些设备通信的设备。

例如, 在通用串行总线 (USB) 或 IEEE 1394 (Firewire) 总线上控制设备的微型端口驱动程序必须在其上边缘公开标准的 NDIS 微型端口驱动程序接口, 并在其下边缘使用特定总线的类接口。 此类微型端口驱动程序通过将 i/o 请求数据包 (Irp) 发送到总线, 与连接到总线的设备进行通信。

以下主题介绍如何实现使用 WDM 下边缘的微型端口驱动程序:

[具有 WDM 下边缘的微型端口驱动程序](miniport-driver-with-a-wdm-lower-edge.md)

[为 WDM 下边缘注册微型端口驱动程序函数](registering-miniport-driver-functions-for-wdm-lower-edge.md)

[使用 WDM 下边缘初始化微型端口驱动程序](initializing-a-miniport-driver-with-a-wdm-lower-edge.md)

[发出命令以与设备通信](issuing-commands-to-communicate-with-devices.md)

[针对 WDM 下边缘的实现提示和要求](implementation-tips-and-requirements-for-wdm-lower-edge.md)

[WDM 下边缘的编译标志](compile-flags-for-wdm-lower-edge.md)

[WDM 下边缘的电源管理](power-management-for-wdm-lower-edge.md)

[安装 NDIS-WDM 微型端口驱动程序](installing-ndis-wdm-miniport-drivers.md)

 

 





