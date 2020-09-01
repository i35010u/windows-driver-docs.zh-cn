---
title: 无法验证设备对象
description: 无法验证设备对象
ms.assetid: aa4abc20-0b87-44d7-8987-a5b2be397bb1
keywords:
- 可靠性 WDK 内核，设备对象验证
- 设备对象 WDK 内核，验证失败
- 验证失败的 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5237d98628f4d71a609348566f95d1a79f7b3a05
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189061"
---
# <a name="failure-to-validate-device-objects"></a>无法验证设备对象





许多驱动程序通过调用 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)来创建多种类型的设备对象。 某些驱动程序在其 **DriverEntry** 例程中创建控制设备对象，以允许应用程序与驱动程序通信，甚至在驱动程序创建 FDO 之前。 例如，当文件系统驱动程序将自身注册为带有 **IoRegisterFileSystem**的文件系统时，文件系统驱动程序将创建设备对象来处理文件系统通知。

对于创建的任何设备对象，驱动程序应准备好 [**IRP \_ MJ \_ CREATE**](./irp-mj-create.md) 请求。 完成成功状态的请求后，驱动程序应会接收对创建的文件对象的任何用户可访问的 i/o 请求。 因此，创建多个设备对象的任何驱动程序都必须检查每个 i/o 请求指定的设备对象。

例如，假设驱动程序在 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)中创建了总体控制设备对象，然后在其 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程中创建了另一组设备对象。 假设 *AddDevice* 例程利用有关较低级别驱动程序的信息来初始化设备扩展，但控制设备对象不包含该信息。 在这种情况下，所有调度例程必须仔细检查它们接收的每个设备对象。 否则，在尝试使用设备扩展信息时，驱动程序可能会崩溃。

 

