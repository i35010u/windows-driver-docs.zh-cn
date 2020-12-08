---
title: 存储类驱动程序的 ClaimDevice 例程
description: 存储类驱动程序的 ClaimDevice 例程
keywords:
- ClaimDevice
- 申报存储设备
- 查询-属性请求 WDK 存储
- 配置信息 WDk 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cc319ea402af4b3f4021dbcc7b146911cf67c7f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806679"
---
# <a name="storage-class-drivers-claimdevice-routine"></a>存储类驱动程序的 ClaimDevice 例程


## <span id="ddk_storage_class_drivers_claimdevice_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_CLAIMDEVICE_ROUTINE_KG"></span>


声明存储设备的 *ClaimDevice* 例程通常是从 [存储类驱动程序的 AddDevice 例程](storage-class-driver-s-adddevice-routine.md)中调用的。

为声明存储设备，类驱动程序通过在 *AddDevice* 调用中通过将 PDO 与类驱动程序一起调用来调用 [**IoGetAttachedDeviceReference**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference)来获取对设备对象的引用，然后从其 *AddDevice* 例程调用内部 *ClaimDevice* 例程，或以内联方式实现相同的功能。 *ClaimDevice* 例程使用 **函数** 值 SRB 函数声明设备设置一个 SRB \_ \_ \_ ，并将其发送到类驱动程序调用 **IoGetAttachedDeviceReference** 返回的设备对象。

*ClaimDevice* 例程使用 [**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)分配 IRP，使用 I/o 控制代码 IOCTL SCSI 来设置端口驱动程序的 i/o 堆栈位置 \_ 。 SCSI \_ 执行 \_ NONE 和指向 SRB 的指针的指针 **。** *ClaimDevice* 还必须使用 **KeInitializeEvent** 设置事件对象，以便它可以等待完成 IRP 的操作。 然后，它会将 IRP 发送到带有 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的下一个较低版本的驱动程序。

IRP 完成后， *ClaimDevice* 应发布对 **IoGetAttachedDeviceReference** 返回的设备对象的引用。

*ClaimDevice* 例程可以将双义务作为要从类驱动程序的 *RemoveDevice* 例程调用的例程，或者，如果驱动程序成功在为设备提供服务，但无法创建设备对象，则可以通过 *AddDevice* 。 在这种情况下， *ClaimDevice* 将使用 **函数** 值 SRB \_ 函数 \_ RELEASE 设备 \_ 发送 SRB。

 

