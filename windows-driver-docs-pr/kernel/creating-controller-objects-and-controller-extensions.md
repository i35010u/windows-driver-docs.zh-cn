---
title: 创建控制器对象和控制器扩展
description: 创建控制器对象和控制器扩展
ms.assetid: 1f5bfcbc-1d8e-4ace-9539-a25e226444a6
keywords:
- 控制器对象 WDK 内核，创建
- IoCreateController
- 控制器扩展 WDK i/o
- 扩展 WDK 控制器对象
- 控制器对象 WDK 内核，扩展
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72588b1b51265bacb337d850812678aa078f0e7c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837014"
---
# <a name="creating-controller-objects-and-controller-extensions"></a>创建控制器对象和控制器扩展





如果驱动程序使用控制器对象，则必须在[**IoCreateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller)创建设备对象之后调用该驱动程序，并且该驱动程序的设备可用于 i/o，通常是在接收 PnP [**IRP 之后\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求。 下图说明了调用。

![阐释控制器对象的关系图](images/3ctlrobj.png)

每个控制器对象都有一个关联的控制器扩展。 如上图所示， **IoCreateController**的调用方确定控制器扩展的*大小*。 其结构和内容是由驱动程序定义的。

除了驱动程序为物理控制器（或带有通道的设备）维护的任何特定于设备的状态信息，上图显示了一组代表控制器扩展的驱动程序定义数据。

**IoCreateController**返回的*PtrToControllerObject*指针必须传入驱动程序对[**IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)和[**IoFreeController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller)的调用，如为[i/o 分配控制器对象中所述。操作](allocating-controller-objects-for-i-o-operations.md)。 驱动程序必须将返回的控制器对象指针存储在其驱动程序创建的设备对象的设备扩展中，或存储在另一个可访问驱动程序的常驻存储区域（由驱动程序分配的非分页池）中。 如果卸载了驱动程序，则还必须将控制器对象指针传递到[**IoDeleteController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iodeletecontroller)。

大多数设置控制器对象的驱动程序都可以轻松地将指向当前目标设备对象或设备扩展的指针存储在控制器扩展中。 通常，此类驱动程序在其每个设备扩展中存储控制器对象指针，使其可以使用*ControllerObject * * *-&gt;ControllerExtension** 指针访问驱动程序维护的、特定于控制器的状态关于 i/o针对每个目标设备对象的操作。

如果控制器对象表示的物理控制器产生中断，则驱动程序还可以使用控制器扩展作为[**IoConnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)返回的*PtrToInterruptObject*指针的存储。 有关详细信息，请参阅[中断服务例程](interrupt-service-routines.md)。

**IoCreateController**为控制器对象和扩展分配驻留存储，并将其初始化为零。 如果无法分配内存，则**IoCreateController**将返回**NULL**指针。 如果出现这种情况，驱动程序必须无法启动设备，并且应返回状态\_\_资源不足。

 

 




