---
title: 使用 Windows Vista 以前的 IoConnectInterruptEx
description: 使用 Windows Vista 以前的 IoConnectInterruptEx
keywords:
- IoConnectInterruptEx
- iointex
- 基于行的中断 WDK 内核
- 消息-已发出信号中断 WDK 内核
- CONNECT_LINE_BASED
- CONNECT_MESSAGE_BASED
- CONNECT_FULLY_SPECIFIED
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f74d6605c2c6cd45ee9c510f08bd14878a02b846
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794819"
---
# <a name="using-ioconnectinterruptex-prior-to-windows-vista"></a>使用 Windows Vista 以前的 IoConnectInterruptEx


Windows 2000、Windows XP 或 Windows Server 2003 的驱动程序可以链接到 Iointex 库，以便在这些版本的操作系统上使用 [**IoConnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex) 。

若要在此类驱动程序中使用 **IoConnectInterruptEx** ，请在该驱动程序的源代码中包括 Iointex，紧跟在 Wdm 或 Ntddk。 Iointex 标头声明例程的原型。 构建驱动程序时，请确保它以静态方式链接到 Iointex。

对于 Windows Vista 之前的操作系统，Iointex 提供的 **IoConnectInterruptEx** 版本仅支持连接 \_ 完全 \_ 指定的例程版本。 如果指定任何其他版本，例程将返回一个 NTSTATUS 错误代码，并将 *参数* - &gt; **版本** 设置为 " \_ 完全 \_ 指定"。

使用此行为，您可以编写您的驱动程序，使其使用基于连接线路的连接 \_ \_ 或 \_ \_ 基于 Windows Vista 的连接消息，并 \_ \_ 在早期的操作系统上完全指定连接。 首先调用 **IoConnectInterruptEx** ，其中的 *参数* - &gt; **版本** 等于 \_ 基于连接行 \_ 或连接 \_ 消息 \_ 。 如果返回值为错误代码，并且 *参数* - &gt; **version** ！ = CONNECT \_ 完全 \_ 指定，则使用 *Parameters* - &gt; 设置为 connect 完全指定的参数 **版本** 重试该操作 \_ \_ 。

下面的代码示例演示了此方法：

```cpp
IO_CONNECT_INTERRUPT_PARAMETERS params;

// deviceExtension is a pointer to the driver's device extension. 
//     deviceExtension->MessageUsed is a BOOLEAN.

RtlZeroMemory( &params, sizeof(IO_CONNECT_INTERRUPT_PARAMETERS) );
params.Version = CONNECT_MESSAGE_BASED;

// Set members of params.MessageBased here.

status = IoConnectInterruptEx(&params);

if ( NT_SUCCESS(status) ) {
    // Operation succeeded. We are running on Windows Vista.
    devExt->MessageUsed = TRUE; // We save this for posterity.
} else {
    // Check to see if we are running on an operating system prior to Windows Vista.
    if (params.Version == CONNECT_FULLY_SPECIFIED) {
        devExt->MessageUsed = FALSE;  // We're not using message-signaled interrupts.
 
        // Set members of params.FullySpecified here.
 
        status = IoConnectInterruptEx(&params);
    } else {
        // Other error.
    }
}
```

 

