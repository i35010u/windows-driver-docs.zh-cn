---
title: 使用 Windows Vista 以前的 IoConnectInterruptEx
description: 使用 Windows Vista 以前的 IoConnectInterruptEx
ms.assetid: a08b2869-93f8-440b-9fbe-068604c6007d
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
ms.openlocfilehash: 5fcca8da985eb669e465112886236dc96010d789
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835990"
---
# <a name="using-ioconnectinterruptex-prior-to-windows-vista"></a>使用 Windows Vista 以前的 IoConnectInterruptEx


Windows 2000、Windows XP 或 Windows Server 2003 的驱动程序可以链接到 Iointex 库，以便在这些版本的操作系统上使用[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex) 。

若要在此类驱动程序中使用**IoConnectInterruptEx** ，请在该驱动程序的源代码中包括 Iointex，紧跟在 Wdm 或 Ntddk。 Iointex 标头声明例程的原型。 构建驱动程序时，请确保它以静态方式链接到 Iointex。

对于 Windows Vista 之前的操作系统，Iointex 提供的**IoConnectInterruptEx**版本仅支持\_完全\_指定的例程版本进行连接。 如果指定任何其他版本，则例程将返回一个 NTSTATUS 错误代码，并将*参数*-&gt;**版本**设置为连接\_完全\_指定。

使用此行为，您可以编写您的驱动程序，以便它使用基于\_行\_的连接，或连接\_基于 Windows Vista 的消息\_，并将\_完全在早期操作系统上指定\_。 首先调用具有*参数*的**IoConnectInterruptEx**&gt;**版本**等于-\_行\_基于或连接\_消息\_。 如果返回值为错误代码，并且*参数*-&gt;**Version** ！ = CONNECT\_完全\_指定，则使用-**版本**设置为 "connect" 的*参数*重试该操作&gt;10_ 已完全\_。

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

 

 




