---
title: 可移植
description: 可移植
ms.assetid: 3ce16503-e375-44c1-82a7-796286c1a253
keywords:
- 可移植的驱动程序 WDK 内核
- 依赖于平台的定义 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f7c351fbb84fd7d343666f502a63a6a3d2fd3d5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369201"
---
# <a name="portable"></a>可移植





所有驱动程序必须跨所有 Windows 支持的硬件平台可移植。 若要实现跨平台可移植性，驱动程序编写人员应：

-   C （没有程序集语言） 中的代码。

-   通过仅使用的编程接口和 WDK 中提供的标头与 Windows 进行交互。

### <a name="coding-drivers-in-c"></a>编码 C 中的驱动程序

应在 C 中编写所有内核模式驱动程序，以便他们可以用系统兼容 C 编译器重新编译、 重新链接，并在不同的 Microsoft Windows 平台上运行而无需重写或替换任何代码。 大多数操作系统组件完全在 C 中，编码的以便跨硬件平台的操作系统是随时可移植程序集语言编写的 HAL 和内核组件仅少量使用。 您不能使用许多C++语言中内核模式驱动程序，因此，应该仔细评估使用的此类构造的构造。 有关驱动程序包括时出现的问题详细信息C++功能，请参阅[C++内核模式驱动程序：优点和缺点](https://go.microsoft.com/fwlink/p/?linkid=56294)白皮书。

如果不能保证这些功能必须由其他系统兼容编译器支持，驱动程序不应依赖于任何特定的系统兼容 C 编译器或 C 支持库的功能。 一般情况下，驱动程序代码应符合 ANSI C 标准，而依赖于此标准描述为"实现定义。"的任何内容

若要编写可移植的驱动程序，最好避免：

-   数据类型可以不同大小或从一个平台到另一个布局中的依赖项。

-   调用对状态进行维护任何标准的 C 运行时库函数。

-   调用的操作系统为其提供一个备用的支持例程的标准 C 运行时库函数。

### <a name="using-wdk-supplied-interfaces"></a>使用 WDK 提供接口

每个 Windows NT executive 组件将内核模式的一组导出[驱动程序支持例程](https://msdn.microsoft.com/library/windows/hardware/ff544200)驱动程序和所有其他内核模式组件调用。 如果随着时间的推移发生更改的支持例程的底层实现，其调用方保持可移植的因为定义组件的接口不会更改。

WDK 提供了一组标头文件，用于定义特定于系统的数据类型和驱动程序 （和所有其他内核模式组件） 用于帮助维护到另一个从一个平台可移植性的常量。 所有内核模式驱动程序都包括一个主 WDK 内核模式标头文件、 wdm.h 中或 Ntddk.h。 不只系统提供的标头定义基本的内核模式类型，但也相应选择任何特定于处理器的体系结构标头时使用相应的编译器指令编译一个驱动程序中拉取的 master 头文件。

某些驱动程序，如[SCSI 微型端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff565309)， [NDIS 驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff556938)，并[微型端口驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff570509)，包括其他系统提供的标头文件。

如果驱动程序需要依赖于平台的定义，最好将这些定义中的隔离 **\#ifdef**语句，以便每个驱动程序可以编译并链接为适当的硬件平台。 但是，您几乎总是可以避免在驱动程序中实现的任何特定于平台的、 有条件地编译代码，通过使用支持例程、 宏、 常量和 WDK master 头文件提供的类型。

内核模式驱动程序可以使用内核模式**Rtl * Xxx*** WDK 中所述的例程。 内核模式驱动程序不能调用用户模式下**Rtl * Xxx*** 例程。

 

 




