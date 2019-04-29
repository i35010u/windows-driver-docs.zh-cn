---
title: 编写 WDM 驱动程序
description: 编写 WDM 驱动程序
ms.assetid: 379305f0-3caa-4c8d-add5-17e8c83f2429
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2b894bcff2e80d3fa24cb2168164efe883632349
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370567"
---
# <a name="writing-wdm-drivers"></a>编写 WDM 驱动程序


本部分讨论的 Microsoft Windows 驱动程序模型 (WDM) 体系结构。 此体系结构开始在 Windows 2000 中为以前的 Windows NT 设备驱动程序的增强功能。

**请注意**  之前不支持 Windows 2000，并应更新这些驱动程序的基于 Windows NT 的操作系统版本的驱动程序。 WDM 体系结构不支持驱动程序 （例如 Windows 98)，非基于 Windows NT 的操作系统，则应重写此类驱动程序。

 

本部分细分为三个部分：

-   [Windows 驱动程序模型](windows-driver-model.md)介绍 Windows 驱动程序模型 (WDM) 包括 WDM 驱动程序、 设备配置和 WDM 版本控制的类型。

-   [设备对象和设备堆栈](device-objects-and-device-stacks.md)介绍设备对象和设备堆栈。 部分包含有关物理设备对象 (PDOs)、 (FDOs) 的功能的设备对象和筛选设备对象 （筛选器 DOs） 的信息。 驱动程序通常由一组协同工作的设备对象。 设备对象的这组称为*堆栈*。 堆栈可以帮助您了解到的信息的流和从驱动程序和驱动程序的不同部分如何进行内部通信。

-   [内核模式驱动程序组件](kernel-mode-driver-components.md)介绍了为功能驱动程序而必须实现的哪些例程是可选的例程。

    一个*设备驱动程序*是一套软件代码，必须将集成到操作系统。 若要完成这种集成，您必须编写的一组处理程序例程中您的驱动程序在进程调用从操作系统。 这些例程可以是简单的函数调用，但其中许多实现处理*I/O 请求数据包*(Irp)，这将简化驱动程序和操作系统之间的通信。

**请注意**  WDM 驱动程序还可以使用 Windows 驱动程序框架 (WDF) 库来轻松地编写设备驱动程序的某些部分。 具体而言，内核模式驱动程序可以使用内核模式驱动程序框架 (KMDF)，它是 WDF 的一部分。 有关 KMDF 内核模式驱动程序的详细信息，请参阅[内核模式驱动程序框架概述](https://msdn.microsoft.com/library/windows/hardware/ff544296)。 请注意 KMDF 不会替换 WDM。 仍必须了解 WDM 编写 KMDF 驱动程序中的不同部分。

 

 

 




