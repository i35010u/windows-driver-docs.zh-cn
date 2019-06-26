---
title: 提供供应商定义的 ACPI 设备接口
description: 提供供应商定义的 ACPI 设备接口
ms.assetid: 5a7fd03b-6d4f-481b-8e4e-0e1deaf88583
keywords:
- ACPI 设备 WDK，设备接口
- 供应商定义的设备接口 WDK ACPI
- 设备接口 WDK ACPI
- 功能的驱动程序 WDK ACPI，供应商定义的设备接口
- WDM 函数驱动程序 WDK ACPI，供应商定义的设备接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24d4b33ce8796b54295f69c5c1e85e7ae66faf65
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355816"
---
# <a name="providing-a-vendor-defined-acpi-device-interface"></a>提供供应商定义的 ACPI 设备接口





供应商可以提供一个可选*设备接口*的自定义 Ioctl 运行 ACPI 设备的功能的设备对象和支持 (*FDO*)。

功能驱动程序通常会调用[ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)中其[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程，以注册设备接口。 驱动程序调用[ **IoSetDeviceInterfaceState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)插启动 FDO 后启用该接口。 如果通过插移除某个设备驱动程序应禁用接口。

设备接口类 GUID 是供应商定义的。

 

 




