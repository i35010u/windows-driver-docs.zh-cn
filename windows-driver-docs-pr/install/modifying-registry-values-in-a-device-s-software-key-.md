---
title: 修改设备的软件键中的注册表值
description: 修改设备的软件键中的注册表值
ms.assetid: 4DBDB53D-CA64-4c19-84A5-FBE1529FD0C5
keywords:
- 修改设备的软件项中的注册表值的注册表 WDK 设备安装
- 修改注册表值 WDK 设备安装，设备软件密钥
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d9b829fed68a0653c733f77d56819fa17263d77
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386231"
---
# <a name="modifying-registry-values-in-a-devices-software-key"></a>修改设备的软件键中的注册表值


您必须修改以下注册表项的值 (*设备属性*) 中的设备*软件密钥*:

-   DriverDate

-   DriverDateData

-   DriverDesc

-   DriverVersion

-   InfPath

-   InfSection

-   InfSectionExt

-   MatchingDeviceId

-   ProviderName

-   EnumPropPages32

这些设备属性表示的设备安装状态。 直接修改这些属性可能导致设备的安装状态无效。 例如，与更改信息相关[INF 文件](overview-of-inf-files.md)使设备和驱动程序签名信息等属性与关联的驱动程序文件的信息。 更改驱动程序版本或驱动程序日期可能会中断 Windows 更新功能。

**请注意**  从 Windows Vista 开始，操作系统施加了"仅安装时间"访问限制为这些属性。 值可以复制的兼容性，并直接修改的值在设备安装过程中不会影响内部状态。

 

若要安全地修改设备的软件密钥中的其他注册表条目的值，请遵循以下准则：

-   使用[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)并[ **SetupDiSetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)检索和设置标准或自定义属性。

    有关详细信息，请参阅[访问设备驱动程序属性](accessing-device-driver-properties.md)。

-   设置由操作系统不保留这些设备属性。

    例如，若要更改显示给用户的设备的名称，更改其[ **DEVPKEY_Device_FriendlyName** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-friendlyname)设备属性。

 

 





