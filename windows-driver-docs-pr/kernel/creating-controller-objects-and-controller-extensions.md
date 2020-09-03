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
ms.openlocfilehash: 96a127e983201973ce8f9b3ffd764128b710cbbb
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403236"
---
# <a name="creating-controller-objects-and-controller-extensions"></a>创建控制器对象和控制器扩展





如果驱动程序使用控制器对象，则必须在 [**IoCreateController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller) 创建设备对象之后调用该驱动程序，并且该驱动程序的设备已准备好进行 i/o，通常是在接收到 PnP [**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md) 请求之后。 下图说明了调用。

![阐释控制器对象的关系图](images/3ctlrobj.png)

每个控制器对象都有一个关联的控制器扩展。 如上图所示， **IoCreateController** 的调用方确定控制器扩展的 *大小* 。 其结构和内容是由驱动程序定义的。

除了驱动程序为物理控制器 (或带有通道) 的设备提供的任何特定于设备的状态信息，上图显示了控制器扩展的一组代表驱动程序定义数据。

**IoCreateController**返回的*PtrToControllerObject*指针必须传入驱动程序对[**IoAllocateController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)和[**IoFreeController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller)的调用，如为[i/o 操作分配控制器对象](allocating-controller-objects-for-i-o-operations.md)中所述。 驱动程序必须将返回的控制器对象指针存储在其驱动程序创建的设备对象的设备扩展中，或存储在驱动程序可访问的另一个可访问的常驻存储区域， (非分页池，由驱动程序) 分配。 如果卸载了驱动程序，则还必须将控制器对象指针传递到 [**IoDeleteController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iodeletecontroller)。

大多数设置控制器对象的驱动程序都可以轻松地将指向当前目标设备对象或设备扩展的指针存储在控制器扩展中。 通常，此类驱动程序会在其每个设备扩展中存储控制器对象指针，使其可以使用 *ControllerObject * * *- &gt; ControllerExtension** 指针来访问驱动程序维护的、特定于控制器的状态关于每个目标设备对象的 i/o 操作。

如果控制器对象表示的物理控制器产生中断，则驱动程序还可以使用控制器扩展作为[**IoConnectInterrupt**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)返回的*PtrToInterruptObject*指针的存储。 有关详细信息，请参阅 [中断服务例程](introduction-to-interrupt-service-routines.md)。

**IoCreateController** 为控制器对象和扩展分配驻留存储，并将其初始化为零。 如果无法分配内存，则 **IoCreateController** 将返回 **NULL** 指针。 如果出现这种情况，驱动程序必须无法启动设备，并且应返回 "状态" \_ \_ 资源不足。

 

