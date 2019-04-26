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
ms.openlocfilehash: 28f13f79930dce8b58de1a07428f9ff0b6ec09e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328826"
---
# <a name="providing-a-vendor-defined-acpi-device-interface"></a>提供供应商定义的 ACPI 设备接口





供应商可以提供一个可选*设备接口*的自定义 Ioctl 运行 ACPI 设备的功能的设备对象和支持 (*FDO*)。

功能驱动程序通常会调用[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)中其[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程，以注册设备接口。 驱动程序调用[ **IoSetDeviceInterfaceState** ](https://msdn.microsoft.com/library/windows/hardware/ff549700)插启动 FDO 后启用该接口。 如果通过插移除某个设备驱动程序应禁用接口。

设备接口类 GUID 是供应商定义的。

 

 




