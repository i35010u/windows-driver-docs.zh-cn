---
title: 注册 ISR
description: 注册 ISR
keywords:
- 中断服务例程 WDK 内核，注册 Isr
- 中断对象 WDK 内核，注册 Isr
- Isr WDK 内核，注册 Isr
- 注册 Isr WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c2887466bcd437c22c66e42389e22c4203b18bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837989"
---
# <a name="registering-an-isr"></a>注册 ISR


驱动程序使用 [**IoConnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex) 例程为中断注册 ISR。 **IoConnectInterruptEx** 是 Windows Vista 和更高版本操作系统的一部分。 **IoConnectInterruptEx** 采用 *单个 parameter 参数，该参数是* 一个指向 [**IO \_ CONNECT \_ 中断 \_ 参数**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_connect_interrupt_parameters) 结构的指针。 对于 Windows Server 2003、Windows XP 和 Windows 2000，驱动程序可以使用 Windows 驱动程序工具包 (WDK) 中包含的 Iointex 库。

在 Windows Vista 和更高版本中， **IoConnectInterruptEx** 提供了几种不同的方法来注册 ISR。 为 *Parameters* 版本指定的值 - &gt; **Version** 将确定方法，如下所示：

-   使用 " \_ 基于连接线路" \_ 为设备的所有基于线路的中断注册 [*InterruptService*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine) 例程。  (设备最多只能有一个基于行的中断。 ) 系统会自动检测分配给设备的任何基于行的中断。 有关详细信息，请参阅 [使用 \_ 基于连接线路 \_ 的 IoConnectInterruptEx 版本](using-the-connect-line-based-version-of-ioconnectinterruptex.md)。

-   使用 " \_ 基于连接的消息" \_ 为所有设备的消息终止中断注册 [*InterruptMessageService*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine) 例程。 你还可以指定回退 [*InterruptService*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine) 例程-如果设备仅具有基于行的中断，则 **IoConnectInterruptEx** 将注册 *InterruptService* 例程。 系统会自动检测分配给设备的任何消息信号中断。 有关详细信息，请参阅 [使用 \_ 基于连接消息 \_ 的 IoConnectInterruptEx 版本](using-the-connect-message-based-version-of-ioconnectinterruptex.md)。

-   使用 " \_ 完全 \_ 指定" 连接，为每个中断单独注册 *InterruptService* 例程。 您可以使用此方法为基于行的或消息发出的中断指定 *InterruptService* 例程，但必须使用 PnP 管理器传递的信息手动指定中断。 有关详细信息，请参阅 [使用 IoConnectInterruptEx 的 CONNECT \_ 完全 \_ 指定版本](using-the-connect-fully-specified-version-of-ioconnectinterruptex.md)。

在 Windows Vista 之前的操作系统上，只能使用 \_ 完全 \_ 指定的连接。 如果指定 "基于连接 \_ 行 \_ 或 \_ 基于消息 \_ 的连接"，则 **IoConnectInterruptEx** 将返回错误。 您可以使用此行为来确定您是在 Windows Vista 还是在以前的系统上运行。 有关详细信息，请参阅 [Windows Vista 之前的使用 IoConnectInterruptEx](using-ioconnectinterruptex-prior-to-windows-vista.md)。

 

