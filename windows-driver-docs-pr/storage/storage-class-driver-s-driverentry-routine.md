---
title: 存储类驱动程序的 DriverEntry 例程
description: 存储类驱动程序的 DriverEntry 例程
keywords:
- DriverEntry WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d87725b99a87a54cb2a8d9f5f970ce6f0ae0d180
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837627"
---
# <a name="storage-class-drivers-driverentry-routine"></a>存储类驱动程序的 DriverEntry 例程


## <span id="ddk_storage_class_drivers_driverentry_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


与任何其他 Windows NT 内核模式的高级驱动程序一样，存储类驱动程序的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程必须执行以下操作：

1.  通过调用 [**IoAllocateDriverObjectExtension**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatedriverobjectextension)分配适当大小的驱动程序对象扩展。

2.  将输入注册表路径复制到驱动程序扩展以供以后使用 (如有必要) 并初始化驱动程序扩展。

3.  在 input driver 对象中定义其调度入口点。

有关 PnP 驱动程序的 **DriverEntry** 例程的详细信息，请参阅 [编写 DriverEntry 例程](../kernel/writing-a-driverentry-routine.md)。

 

