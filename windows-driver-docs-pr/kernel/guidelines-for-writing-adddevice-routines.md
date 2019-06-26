---
title: 有关编写 AddDevice 例程的指导原则
description: 有关编写 AddDevice 例程的指导原则
ms.assetid: 8df36af5-158c-4c14-9fc2-2c3f997c2098
keywords:
- AddDevice 例程 WDK 内核，设计指南
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfb3d1fefa0247baf24e8be5dd2f7e14adf2b6bc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375234"
---
# <a name="guidelines-for-writing-adddevice-routines"></a>有关编写 AddDevice 例程的指导原则





编写时应考虑以下设计准则[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程：

-   如果筛选器驱动程序确定其*AddDevice*例程调用它不需要对服务的设备，筛选器驱动程序必须返回状态\_成功，若要允许设备堆栈要加载的设备的其余部分。 筛选器驱动程序不会不创建设备对象也不会将其附加到设备堆栈;筛选器驱动程序只需返回成功，并允许驱动程序添加到堆栈的其余部分。

-   驱动程序必须提供存储，通常在一个设备对象，任何内核定义的对象和它使用 executive 自旋锁的设备扩展中。 驱动程序还必须提供存储指向从 I/O 管理器或其他系统组件获取特定对象的指针。

    您可能决定为长期的 I/O 缓冲区或后备链列表如分配驱动程序的需求的其他系统空间内存。 如果是这样， *AddDevice*例程可以调用以下例程：

    [**ExAllocatePoolWithTag** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)分页或非分页系统空间内存

    [**ExInitializePagedLookasideList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializepagedlookasidelist)或[ **ExInitializeNPagedLookasideList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinitializenpagedlookasidelist)初始化分页或非分页后备链列表

-   如果驱动程序都有设备专用线程或对任何内核定义调度程序对象，在等待*AddDevice*例程可以初始化[内核调度程序对象](kernel-dispatcher-objects.md)。

-   如果该驱动程序使用任何 executive 自旋锁或为一个中断自旋锁，提供存储空间*AddDevice*例程可初始化这些自旋锁。 请参阅[旋转锁](spin-locks.md)有关详细信息。

-   调用时增强文件打开的安全性[ **IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)。

    指定的文件\_设备\_SECURE\_对的调用上打开特征**IoCreateDevice**。 Windows NT 4.0 SP5 及更高版本支持此特性。 它指示要执行的所有打开请求针对的设备对象的安全检查的 I/O 管理器。 供应商应在调用中指定这一特性**IoCreateDevice**如果文件\_设备\_SECURE\_INF 或设备的 INF 未在设备的安装程序类中设置打开特征驱动程序不执行打开其自己的安全检查。 (有关详细信息，请参阅[控制设备 Namespace 访问](controlling-device-namespace-access.md)。)

    如果驱动程序设置的文件\_设备\_SECURE\_打开特征时，它调用**IoCreateDevice**，I/O 管理器将设备对象的安全描述符应用到任何相对打开或此时会打开尾随文件名。 例如，如果文件\_设备\_SECURE\_用于设置打开\\设备\\foo，并且如果\\设备\\foo 只能打开由管理员，然后\\设备\\foo\\还可以由管理员打开 abc。 I/O 管理器，但是，防止用户以普通用户打开\\设备\\foo 和\\设备\\foo\\abc。

    如果一个设备驱动程序将此特性，则 PnP 管理器会将其传播到所有设备的设备对象。

 

 




