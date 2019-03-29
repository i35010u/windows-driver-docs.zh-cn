---
title: 访问已安装设备接口的属性
description: 访问已安装设备接口的属性
ms.assetid: 4079DD59-878E-4b71-9815-543BA838C56D
keywords:
- 设备接口 WDK 设备安装，访问属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ca0bc49279780ca2150d912a08bc7012e852c66
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576632"
---
# <a name="accessing-the-properties-of-installed-device-interfaces"></a>访问已安装设备接口的属性


若要了解在系统注册的设备接口的属性，您不必须打开、 读取，或通过直接访问注册表写入设备接口子项。 与任何注册表项，如位置、 名称或密钥的格式可能会更改的 Windows 不同版本之间。

使用以下准则来安全地查询和修改设备接口的属性：

-   用户模式应用程序应执行以下步骤：

    1.  使用[ **SetupDiOpenDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff552074)找到设备接口并将其添加到一组的名称。

    2.  使用[ **SetupDiGetDeviceInterfaceDetail** ](https://msdn.microsoft.com/library/windows/hardware/ff551120)才能检索设备接口的详细信息。

        可选*DeviceInfoData*参数将接收[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)接口为其注册的设备元素。

    3.  将永久注册表存储用于设备接口类的自定义设置。 若要执行此操作，请使用[ **SetupDiCreateDeviceInterfaceRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff550967) （若要创建新的注册表项） 或[ **SetupDiOpenDeviceInterfaceRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552075)（若要打开现有的注册表项）。

        若要保存的自定义设置，请使用[RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)后创建的注册表项或将其打开。

-   内核模式驱动程序应使用[ **IoOpenDeviceInterfaceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549433)打开设备接口类的注册表项。

 

 





