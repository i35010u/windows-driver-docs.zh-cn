---
title: 存储类驱动程序的 I/O 请求支持
description: 存储类驱动程序的 I/O 请求支持
ms.assetid: 046b7978-49ee-4e3e-a85f-f6ad327b91bf
keywords:
- 存储类驱动程序 WDK，I/O 请求支持
- 类驱动程序 WDK 存储、 I/O 请求支持
- I/O 请求 WDK 存储
- Irp WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba778556d13fcac51beedfc64d1098f33b80a1d5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368868"
---
# <a name="storage-class-drivers-support-of-io-requests"></a>存储类驱动程序的 I/O 请求支持


## <span id="ddk_storage_class_drivers_support_of_i_o_requests_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_SUPPORT_OF_I_O_REQUESTS_KG"></span>


在设计器的存储设备的全新类型的类驱动程序必须确定一组适当的驱动程序支持，具体取决于设备的性质的 I/O 请求。 通常支持的请求集至少包含下列内容：

[**IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)并且，对于某些设备类型或对称性， [ **IRP\_MJ\_关闭**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)

[**IRP\_MJ\_DEVICE\_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)

[**IRP\_MJ\_读取**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)， [ **IRP\_MJ\_编写**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)，和 / 或

[**IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)

[**IRP\_MJ\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)

[**IRP\_MJ\_SYSTEM\_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)

 

 




