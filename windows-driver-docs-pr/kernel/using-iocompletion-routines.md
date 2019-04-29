---
title: 使用 IoCompletion 例程
description: 使用 IoCompletion 例程
ms.assetid: 07a6e930-eef0-4408-9f71-55a827aa558e
keywords:
- IoCompletion 例程
- 完成 Irp WDK 内核，IoCompletion 例程
- 完成 Irp WDK 内核，调度例程
- 完成 Irp 的调度例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 253099033b27b7a0e2bcaf613c275e92882bf30c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364940"
---
# <a name="using-iocompletion-routines"></a>使用 IoCompletion 例程





监视基于特定于 IRP 的较低级别的更高级别的驱动程序执行特定请求的驱动程序可以有一个或多个[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程。 分配 Irp 发送请求到较低的驱动程序的更高级别的驱动程序必须具有*IoCompletion*例程。

最高级别的或中间驱动[ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)或[ *DispatchWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程是最有可能设置*IoCompletion*例程的 IRP，因为较低级别的驱动程序必须以异步方式处理传输请求。

驱动程序堆栈中的最低级别驱动程序无法注册*IoCompletion*例程。

驱动程序通常不注册*IoCompletion* Irp 的例程与同步 I/O 操作相关联。 例如，更高级别的驾[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程可以分配 IRP 使用[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318). 在这种情况下，调度例程通常不会注册*IoCompletion*例程，因为设备控制请求通常以同步方式处理。 相反，该驱动程序可以分配并初始化一个事件对象，并将其*DispatchDeviceControl*例程可以等待一个事件，它在驱动程序分配 Irp 发送时进行初始化。 通常情况下，更高级别的驱动程序不会注册*IoCompletion* IRP 使用分配的日常[ **IoBuildSynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548330)，出于同样的原因。

本部分包含以下主题：

[注册 IoCompletion 例程](registering-an-iocompletion-routine.md)

[实现 IoCompletion 例程](implementing-an-iocompletion-routine.md)

 

 




