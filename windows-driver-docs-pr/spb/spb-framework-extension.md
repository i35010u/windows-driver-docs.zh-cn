---
title: SPB 框架扩展 (SpbCx)
description: 从 Windows 8 开始， (SpbCx) 的 SPB 框架扩展是系统提供的 Kernel-Mode 驱动程序框架扩展 (KMDF) 。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ee279f962797f9ef5f23f41df4b4f6c06343c80
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804825"
---
# <a name="spb-framework-extension-spbcx"></a>SPB 框架扩展 (SpbCx)


从 Windows 8 开始，SPB 框架扩展 (SpbCx) 是系统提供的针对 [内核模式驱动程序框架](../wdf/index.md) 的扩展 (KMDF) 。 SpbCx 与 [SPB 控制器驱动程序](/previous-versions/hh698221(v=vs.85)) 一起工作，以对连接到 [简单外围总线](/previous-versions/hh450903(v=vs.85)) (SPB) （如 I i2c 或 SPI）的外围设备执行 i/o 操作。

SPB 控制器驱动程序执行所有硬件特定的操作。 这些操作包括访问 SPB 控制器的硬件寄存器，以配置控制器并启动与 SPB 连接的外围设备的总线传输。

SpbCx 执行 SPB 控制器设备所共有的处理任务。 特别是，SpbCx 管理 SPB 控制器的 i/o 请求队列。 这些队列包含附加到总线的外围设备的 i/o 请求。 SPB 控制器的硬件供应商提供了一个 SPB 控制器驱动程序，用于执行处理这些请求所需的所有特定于硬件的操作。

SpbCx 与 SPB 控制器驱动程序之间的责任划分如下：

-   SpbCx 管理所有适用于 SPB 控制器设备类的成员的通用函数。 SpbCx 提供了大部分用于控制器驱动程序的默认请求处理和流控制。 从 Windows 8 开始，SpbCx 是 Windows 操作系统的收件箱组件。

-   SPB 控制器驱动程序管理 SPB 控制器设备中特定于硬件的函数。 硬件供应商为其 SPB 控制器设备提供控制器驱动程序。

SpbCx 和 SPB 控制器驱动程序在内核模式下运行。 SpbCx 是一个框架扩展，而 SPB 控制器驱动程序是一个 KMDF 驱动程序。 SPB 控制器驱动程序调用 SpbCx 设备驱动程序接口中的方法， (DDI) 来执行特定于 SPB 的操作，并调用 KMDF 方法来执行其他更通用的驱动程序功能。 有关生成 KMDF 驱动程序的信息，请参阅 [生成和加载 Framework-Based 驱动程序](../wdf/building-and-loading-a-kmdf-driver.md)。

SPB 控制器驱动程序静态链接到 SpbCx 存根库 Spbcx 中的 DDI 入口点。 在运行时，此库执行必要的驱动程序版本协商以动态链接到用于实现 DDI 的框架扩展模块 Spbcx.sys。 需要 Spbcx.sys 特定版本的 SPB 控制器驱动程序可以安全地链接到版本号较高的 Spbcx.sys 版本。 但是，此驱动程序无法链接到版本号较低的 Spbcx.sys 版本。 SpbCx i/o 请求接口类似向后兼容。

尽管硬件供应商可以选择编写不使用 SpbCx 的单一 SPB 控制器驱动程序，但这样做需要很大的努力。 相比之下，使用 SpbCx 的控制器驱动程序更易于开发，通常更可靠。

 

