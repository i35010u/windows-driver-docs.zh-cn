---
title: 微型端口驱动程序使用 WDM 降低接口
description: 微型端口驱动程序使用 WDM 降低接口
ms.assetid: defa955b-c1d2-4c78-a983-584aedc8a1a3
keywords:
- 微型端口驱动程序 WDK 网络 WDM 低接口
- NDIS 微型端口驱动程序 WDK，WDM 降低接口
- NDIS WDM 微型端口驱动程序 WDK 网络
- WDM 低接口 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3bb792ffb6d3328e33a8fcbcd719e06e1dd75fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545537"
---
# <a name="miniport-drivers-with-a-wdm-lower-interface"></a>微型端口驱动程序使用 WDM 降低接口





与 Microsoft 的微型端口驱动程序[Windows 驱动程序模型](https://msdn.microsoft.com/library/windows/hardware/ff565698)(WDM) 较低接口是也称为*NDIS WDM 微型端口驱动程序*。 此类型的微型端口驱动程序：

-   使用 WDM 下边缘。

-   可以调用 NDIS 和非 NDIS 函数。 但是，只要有可能，微型端口驱动程序应调用 NDIS 函数。

-   可以初始化用于控制该总线的设备连接到特定的总线和通信，这些设备的微型端口实例。

例如，控制上通用串行总线 (USB) 或 IEEE 1394 (Firewire) 总线的设备的微型端口驱动程序必须显示在其上边缘的标准 NDIS 微型端口驱动程序接口，并为特定的总线在其下边缘使用类接口。 这样的微型端口驱动程序与 I/O 请求数据包 (Irp) 发送到总线来连接到总线的设备进行通信。

以下主题介绍如何实现使用 WDM 下边缘的微型端口驱动程序：

[使用 WDM 下边缘的微型端口驱动程序](miniport-driver-with-a-wdm-lower-edge.md)

[注册 WDM 下边缘的微型端口驱动程序函数](registering-miniport-driver-functions-for-wdm-lower-edge.md)

[初始化使用 WDM 下边缘的微型端口驱动程序](initializing-a-miniport-driver-with-a-wdm-lower-edge.md)

[发出命令以与设备通信](issuing-commands-to-communicate-with-devices.md)

[实现技巧和 WDM 下边缘的要求](implementation-tips-and-requirements-for-wdm-lower-edge.md)

[用于 WDM 下边缘编译标志](compile-flags-for-wdm-lower-edge.md)

[WDM 下边缘的电源管理](power-management-for-wdm-lower-edge.md)

[安装 NDIS WDM 微型端口驱动程序](installing-ndis-wdm-miniport-drivers.md)

 

 





