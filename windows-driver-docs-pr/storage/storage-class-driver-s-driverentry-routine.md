---
title: 存储类驱动程序的 DriverEntry 例程
description: 存储类驱动程序的 DriverEntry 例程
ms.assetid: 45e929ff-b4e2-4855-8498-15ec4c30f497
keywords:
- DriverEntry WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 015544b3d16b63e146965c6737d31e3496e4485c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339048"
---
# <a name="storage-class-drivers-driverentry-routine"></a>存储类驱动程序的 DriverEntry 例程


## <span id="ddk_storage_class_drivers_driverentry_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


像任何其他 Windows NT 内核模式更高级别的驱动程序， [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程的存储类驱动程序必须执行以下操作：

1.  通过调用分配一个驱动程序的适当大小的对象扩展[ **IoAllocateDriverObjectExtension**](https://msdn.microsoft.com/library/windows/hardware/ff548233)。

2.  将输入的注册表路径复制到驱动程序扩展以供将来使用 （如有必要） 并初始化该驱动程序扩展。

3.  输入驱动程序对象中定义其调度入口点。

有关即插即用驱动程序的详细信息**DriverEntry**例程，请参阅[编写 DriverEntry 例程](https://msdn.microsoft.com/library/windows/hardware/ff566402)。

 

 




