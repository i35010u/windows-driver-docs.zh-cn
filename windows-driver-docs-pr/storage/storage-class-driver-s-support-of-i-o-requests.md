---
title: 存储类驱动程序的 I/O 请求支持
description: 存储类驱动程序的 I/O 请求支持
ms.assetid: 046b7978-49ee-4e3e-a85f-f6ad327b91bf
keywords:
- 存储类驱动程序 WDK，i/o 请求支持
- 类驱动程序 WDK 存储、i/o 请求支持
- I/o 请求 WDK 存储
- Irp WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f00937da52a082aa1d57dbf7292c3608e13af98
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187505"
---
# <a name="storage-class-drivers-support-of-io-requests"></a>存储类驱动程序的 I/O 请求支持


## <span id="ddk_storage_class_drivers_support_of_i_o_requests_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_SUPPORT_OF_I_O_REQUESTS_KG"></span>


用于全新存储设备类型的类驱动程序的设计器必须确定相应的一组 i/o 请求以便驱动程序支持，具体取决于设备的性质。 要支持的请求集通常至少包含以下内容：

[**IRP \_MJ \_ **](../kernel/irp-mj-create.md)为某些设备类型创建和， [ **IRP \_ mj \_ 关闭**](../kernel/irp-mj-close.md)

[**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md)

[**IRP \_MJ \_ READ**](../kernel/irp-mj-read.md)、 [**IRP \_ MJ \_ WRITE**](../kernel/irp-mj-write.md)或 both

[**IRP \_ MJ \_ PNP**](../kernel/irp-mj-pnp.md)

[**IRP \_ MJ \_ POWER**](../kernel/irp-mj-power.md)

[**IRP \_ MJ \_ 系统 \_ 控件**](../kernel/irp-mj-system-control.md)

 

