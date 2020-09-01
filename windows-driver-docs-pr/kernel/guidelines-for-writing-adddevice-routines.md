---
title: 有关编写 AddDevice 例程的指导原则
description: 有关编写 AddDevice 例程的指导原则
ms.assetid: 8df36af5-158c-4c14-9fc2-2c3f997c2098
keywords:
- AddDevice 例程-WDK 内核，设计指南
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd57bc313e5609ddb225315e78c269e6b3367bcd
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89183874"
---
# <a name="guidelines-for-writing-adddevice-routines"></a>有关编写 AddDevice 例程的指导原则





编写 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程时，请考虑以下设计准则：

-   如果筛选器驱动程序确定其 *AddDevice* 例程是为设备调用的，则该筛选器驱动程序必须返回状态 SUCCESS， \_ 以允许为设备加载其余的设备堆栈。 筛选器驱动程序不会创建设备对象，也不会将其附加到设备堆栈;筛选器驱动程序只返回 success，并允许将其他驱动程序添加到堆栈中。

-   驱动程序必须在设备对象的设备扩展中为其使用的任何内核定义对象和 executive 旋转锁提供存储。 驱动程序还必须为指向从 i/o 管理器或其他系统组件获取的某些对象提供存储空间。

    你可能会决定为驱动程序的需要分配额外的系统空间内存，例如适用于长期 i/o 缓冲区或后备链表列表。 如果是这样， *AddDevice* 例程可以调用以下例程：

    分页或非分页的系统空间内存[**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)

    用于初始化分页或非分页后备链表列表的[**ExInitializePagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializepagedlookasidelist)或[**ExInitializeNPagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)

-   如果驱动程序具有设备专用线程或等待任何内核定义的调度程序对象，则 *AddDevice* 例程可能会初始化 [内核调度程序对象](./introduction-to-kernel-dispatcher-objects.md)。

-   如果驱动程序使用任何执行高速循环锁定或为中断自旋锁提供存储， *AddDevice* 例程可能会初始化这些旋转锁。 有关详细信息，请参阅 [自旋锁](./introduction-to-spin-locks.md) 。

-   调用 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)时，提高文件打开安全性。

    \_ \_ \_ 在对**IoCreateDevice**的调用上指定文件设备安全打开的特性。 Windows NT 4.0 SP5 和更高版本支持此特性。 它指示 i/o 管理器针对所有打开的请求对设备对象执行安全检查。 如果**IoCreateDevice** \_ \_ \_ 未在设备的类安装程序 inf 或设备的 inf 中设置文件设备安全打开特性，并且驱动程序在打开时未执行其自己的安全检查，则供应商应在对 IoCreateDevice 的调用上指定此特性。  (有关详细信息，请参阅 [控制设备命名空间访问](controlling-device-namespace-access.md)。 ) 

    如果驱动程序调用 IoCreateDevice 时，驱动程序将设置文件 \_ 设备 \_ 安全的 \_ 开放特征，则 i/o 管理器会将设备对象的安全描述符应用到任何相对打开或尾随文件名。 **IoCreateDevice** 例如，如果为 \_ \_ \_ 设备 foo 设置了 "文件设备安全打开 \\ \\ "，并且 \\ \\ 只有管理员才能打开 device foo，则 \\ \\ \\ 管理员还可以打开设备 foo abc。 但是，i/o 管理器会阻止普通用户打开 \\ device \\ foo 和 \\ device \\ foo \\ abc。

    如果设备的一个驱动程序设置了此特征，则 PnP 管理器会将其传播到设备的所有设备对象。

 

