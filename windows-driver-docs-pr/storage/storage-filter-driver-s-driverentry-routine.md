---
title: 存储筛选器驱动程序 DriverEntry 例程
description: 存储筛选器驱动程序 DriverEntry 例程
ms.assetid: 801daf42-259d-45ab-a5c5-88acb2d35bef
keywords:
- 存储筛选器驱动程序 WDK DriverEntry
- 筛选器驱动程序 WDK 存储 DriverEntry
- SFD WDK 存储 DriverEntry
- DriverEntry WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ae09667dc7bd14b99fc8628900d2a8211f5d7dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519091"
---
# <a name="storage-filter-drivers-driverentry-routine"></a>存储筛选器驱动程序 DriverEntry 例程


## <span id="ddk_storage_filter_drivers_driverentry_routine_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


像任何其他内核模式驱动程序， [ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)存储筛选器驱动程序 (SFD) 的例程必须输入驱动程序对象中定义其调度和其他入口点。 如果有必要，SFD 可以分配一个驱动程序的适当大小的对象扩展通过调用[ **IoAllocateDriverObjectExtension**](https://msdn.microsoft.com/library/windows/hardware/ff548233)，将输入的注册表路径复制到更高版本使用的驱动程序扩展和如果有，请初始化与其他驱动程序确定的数据，该驱动程序扩展。

有关即插即用驱动程序的详细信息[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)。

 

 




