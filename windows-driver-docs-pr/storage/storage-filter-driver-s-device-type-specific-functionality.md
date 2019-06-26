---
title: 存储筛选器驱动程序的特定于设备类型的功能
description: 存储筛选器驱动程序的特定于设备类型的功能
ms.assetid: ecc0d938-e931-46bd-a1e1-0e6da8e149a4
keywords:
- 存储筛选器驱动程序 WDK、 设备类型特定的功能
- 筛选器驱动程序 WDK 存储设备类型特定的功能
- SFD WDK 存储，设备类型特定的功能
- 设备类型特定的功能 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a75dcb0a1093721f4dfee2e46dffa6aff37a38a8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373189"
---
# <a name="storage-filter-drivers-device-type-specific-functionality"></a>存储筛选器驱动程序的特定于设备类型的功能


## <span id="ddk_storage_filter_drivers_device_type_specific_functionality_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_DEVICE_TYPE_SPECIFIC_FUNCTIONALITY_KG"></span>


具体取决于其设备的性质，存储筛选器驱动程序 (SFD) 可能负责以下设备类型特定的功能：

-   将数据从或为特定于设备的格式转换之前或之后发送传输请求，以降低驱动程序，如果设备处理非标准格式的数据

-   设置与 Srb Irp 端口驱动程序支持的 I/O 控制请求、 驱动程序定义的 I/O 控制请求，或传递请求，根据需要为其设备，并将这些 Irp 发送到下一步低驱动程序

-   修改驱动程序所提供的类 Srb 根据需要为其设备

-   建立超时值的请求

-   提供一个或多个[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程和相应的存储类驱动程序，如处理某些错误情况和需要特殊的特定于设备的请求的重试处理

一般情况下，SFD 具有作为存储类驱动程序的要求特定于设备的方式处理这些请求相同的职责。 存储类驱动程序的所需的功能的讨论，请参阅[存储类驱动程序](storage-class-drivers.md)。

 

 




