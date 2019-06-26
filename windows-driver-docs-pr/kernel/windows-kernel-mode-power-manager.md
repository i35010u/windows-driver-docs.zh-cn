---
title: Windows 内核模式电源管理器
description: Windows 内核模式电源管理器
ms.assetid: 2d39e43a-63a6-4474-a1ed-c24b4526a3f5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0ed9d501b4c486d8bb482bb8faf704524157d86d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374173"
---
# <a name="windows-kernel-mode-power-manager"></a>Windows 内核模式电源管理器


Windows 使用电源管理技术来减少 Pc 的功率消耗常规播发和电池供电的便携式计算机特别。 例如，Windows 计算机可以置于睡眠或休眠状态。 复杂的电源管理系统的计算机设备发展，以便当计算机开始关闭的情况下，或转到更低的能耗，附加的设备，可以也关闭电源以正确的方式，以便不会丢失数据。 但这些设备需要一条警告的电源状态更改，它们可能还需要是告知等待，直到它们可以正确地关闭控制设备的通信循环的一部分。

Windows 内核模式电源管理器管理的支持电源状态更改的所有设备的电源状态的有序地更改。 这通常通过复杂的控制其他设备的设备堆栈。 每个控制设备称为*节点*并且必须具有可处理的通信的电源状态更改向上和向下通过设备堆栈的驱动程序。

如果你正在编写一个驱动程序，可能会受到电源状态更改，您必须能够处理以下类型的驱动程序代码中的信息：

-   系统活动级别。

-   系统电池电量水平。

-   若要关闭、 休眠或进入休眠状态的当前请求。

-   例如，按下电源按钮的用户操作。

-   控件面板设置，例如自动关闭在 10%电池电源。

电源管理器处理使用 Irp 这些请求。 有关 Irp 的详细信息，请参阅[处理 Irp](handling-irps.md)。

电源管理器结合使用策略管理，从而处理电源管理和坐标电源事件，然后生成 Irp 的电源管理。 电源管理器收集请求以更改电源状态，决定中的哪个位置的设备必须具有其电源状态更改，并发送相应的 Irp 告诉适当的驱动程序，使所做的更改 (这反过来会告知子设备以使也进行更改）。 策略管理器系统中监视活动，并集成到电源策略的用户状态、 应用程序状态和设备驱动程序状态。

有关详细信息有关电源管理的详细信息，请参阅[电源管理的 Windows 驱动程序](implementing-power-management.md)。

电源管理器被视为 I/O 管理器的子组件。 有关详细信息，请参阅[Windows I/O 管理器](windows-kernel-mode-i-o-manager.md)。

为电源管理器提供直接的界面的例程通常带有前缀"**Po**"; 例如， **PoSetPowerState**。 电源管理器例程的列表，请参阅[电源管理器例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

Windows 驱动程序框架 (WDF) 提供了一组库进行电源管理更容易。 WDF 的详细信息，请参阅[内核模式驱动程序框架概述](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)。

 

 




