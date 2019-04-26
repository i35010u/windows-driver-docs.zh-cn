---
title: SPB 框架扩展 (SpbCx)
description: 从 Windows 8 开始，存储框架扩展 (SpbCx) 是系统提供的扩展到内核模式驱动程序框架 (KMDF)。
ms.assetid: 84015f3c-ff55-4c1a-bb52-63b6f29b99d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a3392b4f1d79c84c300324ccaf8dfac7668ebdb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325725"
---
# <a name="spb-framework-extension-spbcx"></a>SPB 框架扩展 (SpbCx)


从 Windows 8 开始，存储框架扩展 (SpbCx) 是对系统提供的扩展[内核模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff544296)(KMDF)。 SpbCx 一起使用的工作原理[存储控制器驱动程序](https://msdn.microsoft.com/library/windows/hardware/hh698221)若要执行的已连接到外围设备上的 I/O 操作[简单的外围总线](https://msdn.microsoft.com/library/windows/hardware/hh450903)（存储），如 I²C 或 SPI。

存储控制器驱动程序执行所有特定于硬件的操作。 这些操作包括访问的存储控制器，若要配置控制器并启动总线接收和从存储连接的外围设备的硬件寄存器。

SpbCx 执行普遍适用于存储控制器设备的处理任务。 具体而言，SpbCx 管理存储控制器的 I/O 请求队列。 这些队列包含连接到总线的外围设备的 I/O 请求。 存储控制器的硬件供应商提供的存储控制器驱动程序，可以执行所有处理这些请求所需的特定于硬件的操作。

SpbCx 和存储控制器驱动程序之间的责任的划分如下所示：

-   SpbCx 管理通用的存储控制器设备类的所有成员的泛型函数。 SpbCx 提供许多默认请求处理和流控制的控制器驱动程序。 从 Windows 8 开始，SpbCx 是 Windows 操作系统的收件箱组件。

-   存储控制器驱动程序管理的存储控制器设备中的特定于硬件的函数。 硬件供应商提供其存储控制器设备的控制器驱动程序。

SpbCx 和存储控制器驱动程序在内核模式下运行。 SpbCx 是 framework 扩展，并存储控制器驱动程序是一个 KMDF 驱动程序。 存储控制器驱动程序调用 SpbCx 设备驱动程序接口 (DDI) 中的方法来执行特定于存储的操作，并调用 KMDF 方法来执行其他、 多个通用驱动程序功能。 有关构建 KMDF 驱动程序的信息，请参阅[生成和基于 Framework 的驱动程序加载](https://msdn.microsoft.com/library/windows/hardware/ff540730)。

存储控制器驱动程序静态链接到在 SpbCx 存根 （stub） 库中，Spbcx.lib DDI 入口点。 在运行时，此库执行必要的驱动程序版本协商以动态链接到 framework 扩展模块，Spbcx.sys，实现 DDI。 需要特定版本的 Spbcx.sys 的存储控制器驱动程序可以安全地链接到具有更高版本的版本号的 Spbcx.sys 的版本。 但是，此驱动程序无法链接到 Spbcx.sys 具有较低版本号的版本。 SpbCx I/O 请求接口是同样向后兼容。

尽管硬件供应商具有编写不使用 SpbCx 的整体存储控制器驱动程序的选项，但需要大量精力来执行此操作。 相比之下，使用 SpbCx 控制器驱动程序是更轻松地开发，并且通常更为可靠。

 

 




