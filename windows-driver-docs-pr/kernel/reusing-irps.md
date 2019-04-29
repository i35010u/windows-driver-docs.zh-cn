---
title: 重复使用 IRP
description: 重复使用 IRP
ms.assetid: 19b09cf8-b88d-4808-9af0-038d3d02dceb
keywords:
- Irp WDK 内核，重复使用
- 重复使用 Irp WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0277d837767c058bb7fe6eb50c1234f28967f3d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324542"
---
# <a name="reusing-irps"></a>重复使用 IRP





在某些情况下，驱动程序可以*重用*Irp。 该驱动程序可以分配内存缓冲区，使用它来保存 Irp，因为他们需要创建一个的池。

驱动程序必须不尝试重复使用 Irp 颁发的 I/O 管理器。 具体而言，驱动程序不应尝试重复使用创建的 Irp [ **IoMakeAssociatedIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549397)， [ **IoBuildSynchronousFsdRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548330)， [ **IoBuildAsynchronousFsdRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548310)，或[ **IoBuildDeviceIoControlRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548318)例程。

驱动程序可以安全地重复使用 Irp 他们已创建，按如下所示：

1.  如果驱动程序分配作为原始内存 IRP (例如，通过调用[ **ExAllocatePoolWithTag**](https://msdn.microsoft.com/library/windows/hardware/ff544520))，然后将其与初始化[ **IoInitializeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549315)，则可以安全地调用**IoInitializeIrp**或[ **IoReuseIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549661)重新初始化的内存缓冲区。

2.  Microsoft Windows 2000 和更高版本的操作系统，驱动程序的创建与 IRP [ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)可以通过调用重用 IRP **IoReuseIrp**。

3.  如果驱动程序通过调用分配 IRP **IoAllocateIrp**与*ChargeQuota*参数设置为**FALSE**，然后，可以安全地使用**IoInitializeIrp**若要重新初始化 IRP。 必须在 Windows 98 工作的驱动程序 / 我可以使用此方法作为解决方法。 而严格设计适用于 Windows 2000 和更高版本操作系统的驱动程序应使用前一种方法。

 

 




