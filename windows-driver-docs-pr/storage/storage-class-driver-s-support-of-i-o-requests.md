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
ms.openlocfilehash: a023df0bec38f35033bf5fc7250d767f878d51ad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329612"
---
# <a name="storage-class-drivers-support-of-io-requests"></a>存储类驱动程序的 I/O 请求支持


## <span id="ddk_storage_class_drivers_support_of_i_o_requests_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_SUPPORT_OF_I_O_REQUESTS_KG"></span>


在设计器的存储设备的全新类型的类驱动程序必须确定一组适当的驱动程序支持，具体取决于设备的性质的 I/O 请求。 通常支持的请求集至少包含下列内容：

[**IRP\_MJ\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff550729)并且，对于某些设备类型或对称性， [ **IRP\_MJ\_关闭**](https://msdn.microsoft.com/library/windows/hardware/ff550720)

[**IRP\_MJ\_DEVICE\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff550744)

[**IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)， [ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819)，和 / 或

[**IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff550772)

[**IRP\_MJ\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff550784)

[**IRP\_MJ\_SYSTEM\_CONTROL**](https://msdn.microsoft.com/library/windows/hardware/ff550813)

 

 




