---
title: 提供供应商定义的 ACPI 设备接口
description: 提供供应商定义的 ACPI 设备接口
keywords:
- ACPI 设备 WDK，设备接口
- 供应商定义的设备接口 WDK ACPI
- 设备接口 WDK ACPI
- 函数驱动程序 WDK ACPI，供应商定义的设备接口
- WDM 函数驱动程序 WDK ACPI、供应商定义的设备接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9ebf23604ce03796c36b4503c0074cdcfc59e02
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785061"
---
# <a name="providing-a-vendor-defined-acpi-device-interface"></a>提供供应商定义的 ACPI 设备接口





供应商可以提供一个可选的 *设备接口* ，并支持自定义的 IOCTLs，以便 (*FDO*) 操作 ACPI 设备的功能设备对象。

函数驱动程序通常会在其 [**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程中调用 [**IoRegisterDeviceInterface**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)来注册设备接口。 该驱动程序将调用 [**IoSetDeviceInterfaceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate) ，以便在即插即用启动 FDO 后启用该接口。 如果即插即用删除了设备，则驱动程序应禁用接口。

设备接口类 GUID 是供应商定义的 GUID。

 

