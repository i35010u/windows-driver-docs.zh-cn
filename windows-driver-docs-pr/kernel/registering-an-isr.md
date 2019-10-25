---
title: 注册 ISR
description: 注册 ISR
ms.assetid: 903e5664-2193-4456-b133-bb979d700bdf
keywords:
- 中断服务例程 WDK 内核，注册 Isr
- 中断对象 WDK 内核，注册 Isr
- Isr WDK 内核，注册 Isr
- 注册 Isr WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1e3b1239dad90aaf9ca1cf570de07a6eedb2702
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827570"
---
# <a name="registering-an-isr"></a>注册 ISR


驱动程序使用[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)例程为中断注册 ISR。 **IoConnectInterruptEx**是 Windows Vista 和更高版本操作系统的一部分。 **IoConnectInterruptEx**采用单个*参数*参数，该参数是指向[**IO\_连接\_中断\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_connect_interrupt_parameters)结构的指针。 对于 Windows Server 2003、Windows XP 和 Windows 2000，驱动程序可以使用 Windows 驱动程序工具包（WDK）中包含的 Iointex 库。

在 Windows Vista 和更高版本中， **IoConnectInterruptEx**提供了几种不同的方法来注册 ISR。 为*参数*指定的值-&gt;**版本**确定方法，如下所示：

-   使用 "连接"\_行\_，为设备的所有基于行的中断注册[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)例程。 （设备通常最多具有一个基于行的中断。）系统会自动检测分配给设备的任何基于行的中断。 有关详细信息，请参阅[使用连接\_行\_IoConnectInterruptEx 版本](using-the-connect-line-based-version-of-ioconnectinterruptex.md)。

-   使用连接\_消息\_，为所有设备的消息终止中断注册[*InterruptMessageService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine)例程。 你还可以指定回退[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)例程-如果设备仅具有基于行的中断，则**IoConnectInterruptEx**将注册*InterruptService*例程。 系统会自动检测分配给设备的任何消息信号中断。 有关详细信息，请参阅[使用连接\_基于 IoConnectInterruptEx 的消息\_版本](using-the-connect-message-based-version-of-ioconnectinterruptex.md)。

-   使用连接\_完全\_指定，以便为每个中断单独注册*InterruptService*例程。 您可以使用此方法为基于行的或消息发出的中断指定*InterruptService*例程，但必须使用 PnP 管理器传递的信息手动指定中断。 有关详细信息，请参阅[使用连接\_完全\_指定的 IoConnectInterruptEx 版本](using-the-connect-fully-specified-version-of-ioconnectinterruptex.md)。

在 Windows Vista 之前的操作系统上，只能使用\_完全\_指定连接。 如果指定 "连接\_行\_" 或 "连接\_"\_基于的消息，则**IoConnectInterruptEx**将返回错误。 您可以使用此行为来确定您是在 Windows Vista 还是在以前的系统上运行。 有关详细信息，请参阅[Windows Vista 之前的使用 IoConnectInterruptEx](using-ioconnectinterruptex-prior-to-windows-vista.md)。

 

 




