---
title: 存储类驱动程序的 I/O 请求支持
description: 存储类驱动程序的 I/O 请求支持
keywords:
- 存储类驱动程序 WDK，i/o 请求支持
- 类驱动程序 WDK 存储、i/o 请求支持
- I/o 请求 WDK 存储
- Irp WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fea85b9b6e353d9e615e0e8804598bc3a02a4cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822729"
---
# <a name="storage-class-drivers-support-of-io-requests"></a>存储类驱动程序的 I/O 请求支持


## <span id="ddk_storage_class_drivers_support_of_i_o_requests_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_SUPPORT_OF_I_O_REQUESTS_KG"></span>


用于全新存储设备类型的类驱动程序的设计器必须确定相应的一组 i/o 请求以便驱动程序支持，具体取决于设备的性质。 要支持的请求集通常至少包含以下内容：

[**IRP \_MJ \_**](../kernel/irp-mj-create.md)为某些设备类型创建和， [ **IRP \_ mj \_ 关闭**](../kernel/irp-mj-close.md)

[**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md)

[**IRP \_MJ \_ READ**](../kernel/irp-mj-read.md)、 [**IRP \_ MJ \_ WRITE**](../kernel/irp-mj-write.md)或 both

[**IRP \_ MJ \_ PNP**](../kernel/irp-mj-pnp.md)

[**IRP \_ MJ \_ POWER**](../kernel/irp-mj-power.md)

[**IRP \_ MJ \_ 系统 \_ 控件**](../kernel/irp-mj-system-control.md)

 

