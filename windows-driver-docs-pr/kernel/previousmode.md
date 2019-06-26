---
title: PreviousMode
description: PreviousMode
ms.assetid: 1251cca9-604c-48c0-a136-21dd1fe4fa72
keywords:
- PreviousMode
- RequestorMode
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7c0c749fb110d605c3a69b0b4ed4d0cc7e5fb01
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378821"
---
# <a name="previousmode"></a>PreviousMode


在用户模式应用程序调用**Nt**或**Zw**版本的本机系统服务例程，系统调用机制捕获到内核模式调用线程。 若要指示参数值生成在用户模式下，系统的陷阱处理程序调用集**PreviousMode**字段中[线程对象](introduction-to-thread-objects.md)到调用方的**UserMode**. 本机系统服务例程检查**PreviousMode**调用线程，以确定参数是否从用户模式下源的字段。

如果内核模式驱动程序调用本机系统服务例程并将参数从内核模式源到例程的值，该驱动程序必须确保**PreviousMode**当前线程对象中的字段设置为**KernelMode**。

内核模式驱动程序可以在任意线程的上下文中运行并**PreviousMode**字段的此线程可能会设置为**UserMode**。 在这种情况下，内核模式驱动程序可以调用**Zw**版本的本机系统服务例程，以通知的例程的参数值是来自受信任，内核模式来源。 **Zw**调用将转到重写的瘦包装器函数**PreviousMode**当前线程对象中的值。 该包装器函数设置**PreviousMode**到**KernelMode** ，并调用**Nt**例程的版本。 返回从**Nt**例程，包装函数的版本将还原原始**PreviousMode**线程对象，并返回的值。

内核模式驱动程序可以直接调用**Nt**版本的本机系统服务例程。 当内核模式驱动程序处理可以源自在用户模式下或在内核模式下的 I/O 请求时，该驱动程序可以调用**Nt**例程的版本，以便**PreviousMode**的当前值线程在调用期间保持不变。 **Nt * Xxx*** 例程将检查调用线程**PreviousMode**值以确定参数值是否都可以通过在用户模式应用程序或内核模式组件，并对它们进行处理相应地。

如果内核模式驱动程序调用可能会出错**Nt * Xxx*** 例程并**PreviousMode**当前线程对象中的值不准确地指示参数值是否从用户模式或内核模式源。

例如，假定在内核模式驱动程序运行中的任意线程，并且在上下文**PreviousMode**值此线程设置为**UserMode**。 如果该驱动程序通过内核模式文件句柄[ **NtClose** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)例行，此例程将检查**PreviousMode**值，并决定句柄必须是用户模式句柄。 当**NtClose**找不到句柄在用户模式下句柄表中，它将返回状态\_无效\_句柄错误代码。 同时，该驱动程序泄漏永远不会关闭内核模式句柄。

另举一例，如果的参数**Nt * Xxx*** 例程包含的输入或输出缓冲区，并且如果**PreviousMode** = **UserMode**，例程调用[ **ProbeForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)或[ **ProbeForWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)例程，以验证缓冲区。 如果在用户模式内存中，而不是系统内存中分配缓冲区**ProbeFor * Xxx*** 例程会引发异常，并**Nt * Xxx*** 例程将返回状态\_访问\_冲突错误代码。

如果有必要，驱动程序可以调用[ **ExGetPreviousMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exgetpreviousmode)例程，以获取**PreviousMode**从当前线程对象的值。 或者，驱动程序可以读取**RequestorMode**字段从[ **IRP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp)结构，描述所请求的 I/O 操作。 **RequestorMode**字段包含一份**PreviousMode**请求操作的线程的值。

 

 




