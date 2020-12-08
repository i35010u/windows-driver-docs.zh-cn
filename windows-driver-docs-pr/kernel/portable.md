---
title: 可移植
description: 可移植
keywords:
- 便携驱动程序 WDK 内核
- 平台相关的定义 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c337078601295adbb825c95dbc59502bde0240cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814293"
---
# <a name="portable"></a>可移植





所有驱动程序都必须可在所有支持 Windows 的硬件平台上移植。 要实现跨平台可移植性，驱动程序编写人员应：

-   C 中的代码 (不) 汇编语言。

-   仅使用在 WDK 中提供的编程接口和标头与 Windows 交互。

### <a name="coding-drivers-in-c"></a>C 中的编码驱动程序

所有内核模式驱动程序都应该用 C 编写，以便能够使用与系统兼容的 C 编译器重新编译、重新链接并在不同的 Microsoft Windows 平台上运行，而无需重写或替换任何代码。 大多数操作系统组件都是完全在 C 中进行编码的，只有少量的 HAL 和内核组件以汇编语言编写，才能使操作系统在硬件平台之间随时可以移植。 你不能在内核模式驱动程序中使用许多 c + + 语言构造，因此应该谨慎使用此类构造进行评估。 有关驱动程序包含 c + + 功能时出现的问题的详细信息，请参阅 [用于内核模式驱动程序的 c + +：优点和缺点](https://go.microsoft.com/fwlink/p/?linkid=56294) 白皮书。

如果驱动程序不保证其他系统兼容的编译器支持这些功能，驱动程序不应依赖于任何特定于系统兼容的 C 编译器或 C 支持库的功能。 通常，驱动程序代码应符合 ANSI C 标准，而不依赖于此标准将其描述为 "实现定义的任何内容"。

若要编写可移植的驱动程序，最好避免：

-   数据类型依赖于不同平台的大小或布局的依赖项。

-   调用维护状态的任何标准 C 运行时库函数。

-   调用操作系统为其提供备用支持例程的任何标准 C 运行时库函数。

### <a name="using-wdk-supplied-interfaces"></a>使用 WDK-Supplied 接口

每个 Windows NT executive 组件都将导出一组内核模式 [驱动程序支持例程](/windows-hardware/drivers/ddi/index) ，驱动程序和所有其他内核模式组件都调用。 如果支持例程的基础实现随时间而变化，则其调用方将保持可移植，因为定义组件的接口不会更改。

WDK 提供一组头文件，用于定义特定于系统的数据类型和常量，驱动程序 (和其他所有内核模式组件都) 使用该组件来帮助保持从一个平台到另一个平台的可移植性。 所有内核模式驱动程序都包括一个主 WDK 内核模式标头文件（Wdm .h 或 Ntddk）。 主头文件不仅纳入系统提供的标头，用于定义基本内核模式类型，还提取驱动程序使用相应的编译器指令编译时的任何特定于处理器体系结构的标头。

某些驱动程序，如 [SCSI 微型端口驱动程序](../storage/scsi-miniport-drivers.md)、 [NDIS 驱动](/previous-versions/windows/hardware/network/ff556938(v=vs.85))程序和 [视频微型端口驱动程序](../display/video-miniport-drivers-in-the-windows-2000-display-driver-model.md)，包括其他系统提供的标头文件。

如果驱动程序需要与平台相关的定义，最好将这些定义隔离于 **\# ifdef** 语句中，以便可以针对相应的硬件平台编译和链接每个驱动程序。 不过，您几乎始终可以通过使用 WDK 主头文件提供的支持例程、宏、常量和类型来避免在驱动程序中实现任何特定于平台的、有条件地编译代码。

内核模式驱动程序可以使用 WDK 中记录的内核模式 **Rtl * Xxx*** 例程。 内核模式驱动程序无法调用用户模式 **Rtl * Xxx*** 例程。

 

