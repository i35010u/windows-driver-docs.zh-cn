---
title: 创建控制器对象和控制器扩展
description: 创建控制器对象和控制器扩展
ms.assetid: 1f5bfcbc-1d8e-4ace-9539-a25e226444a6
keywords:
- 控制器对象 WDK 内核，创建
- IoCreateController
- 控制器扩展 WDK I/O
- 扩展 WDK 控制器对象
- 控制器对象 WDK 内核扩展
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37ed64eaa342752f35b13afc76059c5ce588c3bb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377185"
---
# <a name="creating-controller-objects-and-controller-extensions"></a>创建控制器对象和控制器扩展





如果驱动程序将使用控制器对象，它必须调用[ **IoCreateController** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatecontroller)它已创建设备对象并且其设备已准备就绪的 I/O，通常接收即插即用后[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求。 下图阐释了调用。

![说明控制器对象的关系图](images/3ctlrobj.png)

每个控制器对象具有关联的控制器扩展。 上一图所示的调用方**IoCreateController**确定*大小*的控制器扩展。 其结构和内容是驱动程序定义的。

除了任何特定于设备的驱动程序有关的物理控制器 （或频道的设备） 上, 图中保持的状态信息显示了具有代表性的一组驱动程序定义数据的控制器扩展。

*PtrToControllerObject*返回的指针**IoCreateController**，必须对驱动程序的调用中传递[ **IoAllocateController** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioallocatecontroller)并[ **IoFreeController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iofreecontroller)中所述[分配 I/O 操作的控制器对象](allocating-controller-objects-for-i-o-operations.md)。 该驱动程序必须在其驱动程序创建的设备对象的设备扩展或另一个驱动程序可访问驻留的存储区域 （非分页池，分配由驱动程序） 中存储返回的控制器对象指针。 如果卸载该驱动程序，它还必须在控制器对象将指针传递到[ **IoDeleteController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iodeletecontroller)。

设置控制器对象的大多数驱动程序查找可以方便地将指向当前的目标设备对象或设备扩展的存储在控制器扩展。 此类驱动程序通常情况下，以便它可以使用将控制器对象指针存储在其设备扩展的每个*ControllerObject * * *-&gt;ControllerExtension** 指针，指向维护驱动程序的访问权限为每个目标设备对象的 I/O 操作的特定于控制器的状态。

如果控制器对象所表示的物理控制器产生中断，驱动程序还可以使用控制器扩展为适用于存储*PtrToInterruptObject*返回的指针[ **IoConnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterrupt)。 有关详细信息，请参阅[中断服务例程](interrupt-service-routines.md)。

**IoCreateController**分配驻留的存储控制器对象和扩展，它可以用零初始化。 如果它无法分配内存， **IoCreateController**返回**NULL**指针。 如果发生这种情况，该驱动程序必须失败设备启动，并且应返回状态\_不足\_资源。

 

 




