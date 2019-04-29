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
ms.openlocfilehash: 4b554d7fa21a48b6806b54f1b39671f83fcb69ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382647"
---
# <a name="registering-an-isr"></a>注册 ISR


驱动程序使用[ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)例程，以注册 ISR 中断。 **IoConnectInterruptEx**是 Windows Vista 和更高版本操作系统的一部分。 **IoConnectInterruptEx**采用单个*参数*参数，它是一个指针，到[ **IO\_CONNECT\_中断\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff550541)结构。 对于 Windows Server 2003、 Windows XP 和 Windows 2000，驱动程序可以使用 Iointex.lib 库包含 Windows Driver Kit (WDK) 中。

Windows Vista 及更高版本， **IoConnectInterruptEx**提供几种不同方法，用于注册 ISR. 为指定的值*参数*-&gt;**版本**确定的方法，按如下所示：

-   使用 CONNECT\_行\_基于注册[ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)所有设备的基于线条的中断例程。 （设备通常具有最多个基于行的中断。）系统会自动检测到分配给设备的任何基于行的中断。 有关详细信息，请参阅[使用 CONNECT\_行\_基于版本的 IoConnectInterruptEx](using-the-connect-line-based-version-of-ioconnectinterruptex.md)。

-   使用 CONNECT\_消息\_基于注册[ *InterruptMessageService* ](https://msdn.microsoft.com/library/windows/hardware/ff547940)所有设备的消息信号中断例程。 此外可以指定回退[ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)例程 — 如果设备仅具有基于行的中断**IoConnectInterruptEx**注册*InterruptService*例程相反。 系统会自动检测到分配给设备的任何消息信号中断。 有关详细信息，请参阅[使用 CONNECT\_消息\_基于版本的 IoConnectInterruptEx](using-the-connect-message-based-version-of-ioconnectinterruptex.md)。

-   使用 CONNECT\_完全\_指定要注册*InterruptService*单独为每个例程中断。 可以使用此指定*InterruptService*例程是基于行的或的消息信号中断，但您必须手动指定使用由即插即用管理器传递信息的中断。 有关详细信息，请参阅[使用 CONNECT\_完全\_指定版本的 IoConnectInterruptEx](using-the-connect-fully-specified-version-of-ioconnectinterruptex.md)。

在 Windows Vista 之前的操作系统，仅可以使用 CONNECT\_完全\_指定。 如果指定连接\_行\_基于或 CONNECT\_消息\_基于**IoConnectInterruptEx**返回错误。 此行为可用于确定是否在 Windows Vista 或更早的系统上运行。 有关详细信息，请参阅[使用之前为 Windows Vista 的 IoConnectInterruptEx](using-ioconnectinterruptex-prior-to-windows-vista.md)。

 

 




