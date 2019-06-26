---
title: 存储类驱动程序的 DriverEntry 例程
description: 存储类驱动程序的 DriverEntry 例程
ms.assetid: 45e929ff-b4e2-4855-8498-15ec4c30f497
keywords:
- DriverEntry WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5cbd50daa298ad6ba550ad518551f281d517ed3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379087"
---
# <a name="storage-class-drivers-driverentry-routine"></a>存储类驱动程序的 DriverEntry 例程


## <span id="ddk_storage_class_drivers_driverentry_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


像任何其他 Windows NT 内核模式更高级别的驱动程序， [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程的存储类驱动程序必须执行以下操作：

1.  通过调用分配一个驱动程序的适当大小的对象扩展[ **IoAllocateDriverObjectExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatedriverobjectextension)。

2.  将输入的注册表路径复制到驱动程序扩展以供将来使用 （如有必要） 并初始化该驱动程序扩展。

3.  输入驱动程序对象中定义其调度入口点。

有关即插即用驱动程序的详细信息**DriverEntry**例程，请参阅[编写 DriverEntry 例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-a-driverentry-routine)。

 

 




