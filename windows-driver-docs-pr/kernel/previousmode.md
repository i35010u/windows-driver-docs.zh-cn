---
title: PreviousMode
description: PreviousMode
ms.assetid: 1251cca9-604c-48c0-a136-21dd1fe4fa72
keywords:
- PreviousMode
- Irp->requestormode
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ede78ca07a562360d9cb170109f1c38f4374497
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838494"
---
# <a name="previousmode"></a>PreviousMode


用户模式应用程序调用本机系统服务例程的**Nt**或**Zw**版本时，系统调用机制会将调用线程捕获到内核模式。 为了指示参数值在用户模式下生成，系统调用的陷阱处理程序会将调用方的[线程对象](introduction-to-thread-objects.md)中的**PreviousMode**字段设置为**UserMode**。 本机系统服务例程检查调用线程的**PreviousMode**字段，以确定参数是否来自用户模式源。

如果内核模式驱动程序调用本机系统服务例程并将参数值传递给来自内核模式源的例程，则驱动程序必须确保将当前线程对象中的**PreviousMode**字段设置为**KernelMode**。

内核模式驱动程序可在任意线程的上下文中运行，此线程的**PreviousMode**字段可能设置为**UserMode**。 在这种情况下，内核模式驱动程序可以调用本机系统服务例程的**Zw**版本来通知例程参数值来自受信任的内核模式源。 **Zw**调用将转到一个精简包装函数，该函数将重写当前 thread 对象中的**PreviousMode**值。 包装函数将**PreviousMode**设置为**KernelMode** ，并调用例程的**Nt**版本。 从例程的**Nt**版本返回时，包装函数将还原 thread 对象的原始**PreviousMode**值，并返回。

内核模式驱动程序可以直接调用本机系统服务例程的**Nt**版本。 当内核模式驱动程序处理可在用户模式或内核模式下发出的 i/o 请求时，驱动程序可以调用例程的**Nt**版本，以便当前线程的**PreviousMode**值在调用期间保持不变。 **Nt * Xxx*** 例程检查调用线程的**PreviousMode**值，以确定参数值是来自用户模式应用程序还是内核模式组件，并相应地对其进行处理。

如果内核模式驱动程序调用**Nt * Xxx*** 例程，并且当前线程对象中的**PreviousMode**值不能准确地指示参数值是来自用户模式还是内核模式源，则会发生错误。

例如，假定内核模式驱动程序在任意线程的上下文中运行，并且此线程的**PreviousMode**值设置为**UserMode**。 如果驱动程序将内核模式文件句柄传递到[**NtClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)例程，此例程会检查**PreviousMode**值并确定该句柄必须是用户模式句柄。 当**NtClose**在用户模式句柄表中找不到句柄时，将返回状态\_无效\_处理错误代码。 同时，驱动程序会泄漏未关闭的内核模式句柄。

例如，如果**Nt * Xxx*** 例程的参数包括输入或输出缓冲区，并且如果**PreviousMode** = **UserMode**，则例程将调用[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)或[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)例程来验证缓冲区。 如果缓冲区是在系统内存而不是在用户模式内存中分配的，则**ProbeFor * xxx*** 例程会引发异常，并且**Nt * xxx*** 例程会返回状态\_访问\_冲突错误代码。

如果需要，驱动程序可以调用[**ExGetPreviousMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exgetpreviousmode)例程，从当前线程对象获取**PreviousMode**值。 或者，驱动程序可以从描述所请求的 i/o 操作的[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)结构读取**irp->requestormode**字段。 **Irp->requestormode**字段包含请求操作的线程的**PreviousMode**值的副本。

 

 




