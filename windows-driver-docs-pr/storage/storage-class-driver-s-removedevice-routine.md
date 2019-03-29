---
title: 存储类驱动程序的 RemoveDevice 例程
description: 存储类驱动程序的 RemoveDevice 例程
ms.assetid: fbcbfbab-676a-43d3-aa63-0ea5e5f265d2
keywords:
- RemoveDevice
- 查询-删除请求 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3deba68f840c7b39c8607d521bccdc1b5f048f44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565158"
---
# <a name="storage-class-drivers-removedevice-routine"></a>存储类驱动程序的 RemoveDevice 例程


## <span id="ddk_storage_class_drivers_removedevice_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_REMOVEDEVICE_ROUTINE_KG"></span>


PnP 管理器时要删除设备，首先调用的类驱动程序[ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程与即插即用的查询删除请求 (IRP\_MJ\_与PNP[ **IRP\_MN\_查询\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551705)。 存储类驱动程序应会在以下情况下的任何查询删除请求失败：

-   设备包含系统页面文件或休眠文件。

-   该驱动程序正在运行较长的操作，这不应取消 （例如，后退或格式设置磁带）。

-   有未完成的句柄 （创建） 的设备。

存储类驱动程序可能还无法满足该查询删除请求设备声明为故障转储，如果因为删除此类设备禁用故障转储。

如果存储类驱动程序将返回状态\_SUCCESS 作为响应查询删除请求，即插即用管理器，然后调用类驱动程序*DispatchPnP*例程与即插即用的删除请求 (IRP\_MJ\_与 PNP [ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738))。 存储类驱动程序*DispatchPnP*日常操作会调用内部*RemoveDevice*例程或实现相同功能内联。

存储类驱动程序的*RemoveDevice*例程必须执行以下操作：

-   释放所有未完成的资源，例如内存或驱动程序分配的事件。

-   如果驱动程序创建的任何操作，，删除符号链接。

-   删除设备对象 (FDO)。

-   将请求转发到下一步低驱动程序。

如果存储类驱动程序在启动时 （例如，若要表示已分区的媒体设备上的分区） 创建 PDOs，此类 PDOs 已被删除时的即插即用的管理器将删除请求发送到的存储类驱动程序。

即使设备对象已被删除，如果它具有非零值的引用计数的设备对象仍然存在系统中，直到其引用计数达到零时后，然后以无提示方式消失。 存储类驱动程序必须尝试删除的设备对象后使用的设备对象指针。

有关处理删除请求的详细信息，请参阅[删除设备](https://msdn.microsoft.com/library/windows/hardware/ff561046)。

 

 




