---
title: 存储类驱动程序的 ClaimDevice 例程
description: 存储类驱动程序的 ClaimDevice 例程
ms.assetid: 175b9be6-34a5-4d20-970c-aa9a6880c242
keywords:
- ClaimDevice
- 声明存储设备
- 查询属性请求 WDK 存储
- WDk 存储的配置信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 604ef785fe4feeeb625ddbd3cbfce412749789d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339039"
---
# <a name="storage-class-drivers-claimdevice-routine"></a>存储类驱动程序的 ClaimDevice 例程


## <span id="ddk_storage_class_drivers_claimdevice_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_CLAIMDEVICE_ROUTINE_KG"></span>


*ClaimDevice*例程，用于对声明的存储设备，通常称为从[存储类驱动程序 AddDevice 例程](storage-class-driver-s-adddevice-routine.md)。

若要声明的存储设备，类驱动程序对设备对象的引用通过调用来获取[ **IoGetAttachedDeviceReference** ](https://msdn.microsoft.com/library/windows/hardware/ff549145)与传递给的类驱动程序中的 PDO *AddDevice*调用，则操作会调用内部*ClaimDevice*例程从其*AddDevice*例程或实现相同功能内联。 一个*ClaimDevice*例程设置 SRB**函数**值 SRB\_函数\_声明\_设备并将其发送到的设备对象返回的类驱动程序的调用**IoGetAttachedDeviceReference**。

*ClaimDevice*例程分配与 IRP [ **IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)、 设置端口驱动程序的 I/O 堆栈位置使用的 I/O 控制代码 IOCTL\_SCSI\_EXECUTE\_NONE 和指向在 SRB **Parameters.Scsi.Srb**。 *ClaimDevice*还必须设置一个事件对象与**KeInitializeEvent**以便它可以等待的 IRP 完成。 然后，它将发送到下一步低驱动程序和 IRP [ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)。

完成 IRP *ClaimDevice*应释放对返回的设备对象的引用**IoGetAttachedDeviceReference**。

一个*ClaimDevice*例程可以充当要从类驱动程序调用的例程 double 值班*RemoveDevice*例程，或从*AddDevice*如果驱动程序成功声明该设备，但不能创建一个设备对象。 在这种情况下， *ClaimDevice*发送与 SRB**函数**值 SRB\_函数\_版本\_设备。

 

 




