---
title: 用于蓝牙功率控制处理的传输总线驱动程序指南
description: Ihv 需要实施传输总线驱动程序，以便支持通常在芯片（SoC）系统上集成的多功能控制器的蓝牙功能。
ms.assetid: 00792128-320E-45C1-9F58-343B72565CA7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52ce7ae24931875f18e3568ca169891ebffc0ed9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834532"
---
# <a name="transport-bus-driver-for-bluetooth-power-control-handling-guidelines"></a>用于蓝牙功率控制处理的传输总线驱动程序指南


Ihv 需要实施传输总线驱动程序，以便支持通常在芯片（SoC）系统上集成的多功能控制器的蓝牙功能。

[蓝牙串行 HCI 总线驱动程序](https://go.microsoft.com/fwlink/p/?linkid=256088)示例可以帮助 ihv 开发其传输总线驱动程序。 此示例演示如何处理来自其上层的 IOCTL （IO 控制）请求，以及如何将 HCI 数据包传送到其下一层的串行控制器驱动程序。 但是，不使用其自己的 IO 传输（在 WDK 示例中为 UART）以外的带外控件通常用于支持空闲控件和唤醒控件;这种机制是必需的，用于优化功率消耗。 本部分及其副标题的信息通过提供处理电源控制的准则和代码示例来补充总线示例驱动程序。

本节中的信息及其副标题适用于：

-   Windows 8.1

通常，蓝牙是一种用于在芯片（SoC）系统上集成的多功能控制器中的一种短范围无线广播。 以前版本的 Windows （最高为 Windows 7）提供了一个收件箱类驱动程序，将 USB 作为唯一的传输选项。 Windows 8 引入了[蓝牙可扩展传输 IOCTLs](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。 在 Windows 8.1 中将继续支持 USB 传输和可扩展传输模型。 扩展性模型 DDI 在 Windows 中保持不变，为系统集成商提供选择合适的 SoC 平台传输的灵活性，例如 UART （通用异步接收器/发送器）。 此外，更简单、低功耗控制器（例如 GPIOs）可用作处理电源控制的 "sideband" 机制（例如，启用蓝牙无线电，作为睡眠/唤醒信号）。

本节中的信息及其子主题提供了此类总线驱动程序的电源控制处理的准则和示例代码，并说明了与蓝牙核心驱动程序的交互。 这些控件包括：空闲功能、武装和 disarming 用于唤醒、空闲和唤醒信号以及设备电源状态更改。 驱动程序开发人员可以采用蓝牙串行 HCI 总线驱动程序示例，简化通过备用（非 USB）传输来支持蓝牙的开发工作。

当使用不同的传输支持蓝牙时，蓝牙 DDIs 对于蓝牙配置文件驱动程序保持不变。 这意味着，蓝牙配置文件驱动程序和应用程序在正在实现的传输或电源控制处理中保持不可知。

 

 





