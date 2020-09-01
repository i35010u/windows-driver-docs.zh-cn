---
title: 编写 WDM 驱动程序
description: 编写 WDM 驱动程序
ms.assetid: 379305f0-3caa-4c8d-add5-17e8c83f2429
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6b51b60083bf43695fa11b22377913f34e3b2e07
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187135"
---
# <a name="writing-wdm-drivers"></a>编写 WDM 驱动程序


本部分讨论 Microsoft Windows 驱动模型 (WDM) 体系结构。 此体系结构在 Windows 2000 中启动，作为对以前的 Windows NT 设备驱动程序的增强功能。

**注意**   不支持 Windows 2000 之前版本的基于 Windows NT 的操作系统的驱动程序，你应该更新这些驱动程序。 对于非基于 Windows NT 的操作系统 (（如 Windows 98) ），WDM 体系结构不支持驱动程序，应重写此类驱动程序。

 

本部分分为三部分：

-   [Windows 驱动模型](windows-driver-model.md) 描述了 wdm) 的 Windows 驱动模型 (，包括 wdm 驱动程序的类型、设备配置和 WDM 版本控制。

-   [设备对象和设备堆栈](device-objects-and-device-stacks.md) 介绍了设备对象和设备堆栈。 本部分包括有关 (PDOs) 、功能设备对象 (FDOs) 的物理设备对象的信息，以及 (筛选器 DOs) 筛选设备对象。 驱动程序通常是从一起工作的一组设备对象生成的。 这组设备对象称为 *堆栈*。 堆栈可帮助您了解驱动程序与驱动程序之间的流动以及驱动程序的不同部分在内部的通信方式。

-   [内核模式驱动程序组件](kernel-mode-driver-components.md) 描述必须实现哪些例程才能具有功能驱动程序，哪些例程是可选的。

    *设备驱动程序*是必须集成到操作系统中的一组软件代码。 若要完成此集成，必须在驱动程序中编写一组处理程序例程来处理来自操作系统的调用。 这些例程可以是简单的函数调用，但其中的许多例程实现 (Irp) 处理 *i/o 请求数据包* ，从而促进驱动程序和操作系统之间的通信。

**注意**   WDM 驱动程序还可以使用 Windows 驱动程序框架 (WDF) 库，使设备驱动程序的某些部分更易于编写。 具体而言，内核模式驱动程序可以使用内核模式驱动程序框架 (KMDF) ，这是 WDF 的一部分。 有关内核模式驱动程序的 KMDF 的详细信息，请参阅 [内核模式驱动程序框架概述](../wdf/index.md)。 请注意，KMDF 不会替换 WDM。 你仍必须了解 WDM 的许多部分，以编写 KMDF 驱动程序。

 

 

