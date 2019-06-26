---
title: 用于蓝牙功率控制处理的传输总线驱动程序指南
description: Ihv 需要实现传输总线驱动程序支持多功能控制器通常集成中的系统芯片 (SoC) 系统上的蓝牙功能。
ms.assetid: 00792128-320E-45C1-9F58-343B72565CA7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 447c19151d1f2a61f23d29c42ab1ce6b3c4a9df8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353997"
---
# <a name="transport-bus-driver-for-bluetooth-power-control-handling-guidelines"></a>用于蓝牙功率控制处理的传输总线驱动程序指南


Ihv 需要实现传输总线驱动程序支持多功能控制器通常集成中的系统芯片 (SoC) 系统上的蓝牙功能。

[蓝牙串行 HCI 总线驱动程序](https://go.microsoft.com/fwlink/p/?linkid=256088)示例可帮助 Ihv 简化的开发其传输总线驱动程序。 此示例说明了如何处理来自其上层 IOCTL （IO 控制） 请求以及如何将 HCI 数据包传递到其串行控制器的驱动程序在其下一层。 但是，而不是使用其自己的 IO 传输 (UART 在 WDK 示例的情况下) 的带外控件通常用于支持空闲状态并唤醒控件;此类机制是所需的可用来优化电源消耗。 在本部分和及其子主题的信息补充总线示例驱动程序通过提供用于处理电源控制的指导原则和示例代码。

在本部分和及其子主题的信息适用于：

-   Windows 8.1

为无线广播，蓝牙通常是集成在芯片 (SoC) 系统上的系统的多功能控制器内的某个函数的短范围。 早期版本的 Windows，直到 Windows 7 提供的收件箱类驱动程序对使用 USB 蓝牙作为唯一的传输选项。 Windows 8 引入[蓝牙可扩展传输 Ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。 USB 传输和可扩展传输模型将继续支持在 Windows 8.1 中。 若要使灵活地选择适合传输对于 SoC 平台，例如 UART （通用异步接收器/转换器） 的系统集成商的 Windows 中，DDI 的可扩展性模型将保持不变。 此外，更简单和低能耗控制器，例如 GPIOs，可以用作处理电源控制"旁带"机制 (例如，启用蓝牙无线和为睡眠/唤醒信号)。

在本部分和及其子主题的信息提供电源控制处理此类总线驱动程序的指导原则和示例代码，并说明与蓝牙核心驱动程序的交互。 控件包括： 空闲的功能，武装和 disarming 唤醒，空闲和信号唤醒，以及设备电源状态更改。 驱动程序开发人员可以采用蓝牙串行 HCI 总线驱动程序示例来简化开发工作，从而通过备用 (非 USB) 传输支持蓝牙。

而要使用不同的传输来支持蓝牙，蓝牙 DDIs 中保持不变蓝牙配置文件驱动程序。 这意味着蓝牙配置文件驱动程序和应用程序保持不可知的处理实现传输或电源控制。

 

 





