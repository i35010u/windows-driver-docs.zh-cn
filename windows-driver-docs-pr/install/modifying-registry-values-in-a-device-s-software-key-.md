---
title: 修改设备的软件键中的注册表值
description: 修改设备的软件键中的注册表值
ms.assetid: 4DBDB53D-CA64-4c19-84A5-FBE1529FD0C5
keywords:
- 注册表 WDK 设备安装，修改设备的软件密钥中的注册表值
- 修改注册表值 WDK 设备安装，设备软件密钥
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b51b5d3ea4bed5c98b1e09752a72c986be6d717a
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095901"
---
# <a name="modifying-registry-values-in-a-devices-software-key"></a>修改设备的软件键中的注册表值


不得在设备的*软件密钥*)  (*设备属性*中修改以下注册表项的值：

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

这些设备属性表示设备的安装状态。 直接修改这些属性可能会使设备的安装状态无效。 例如，更改与 [INF 文件](overview-of-inf-files.md) 相关的信息会使与此类属性相关联的驱动程序文件的信息失效，作为设备和驱动程序的签名信息。 更改驱动程序版本或驱动程序日期可能会损坏 Windows 更新功能。

**注意**   从 Windows Vista 开始，操作系统对这些属性施加 "仅安装时间" 访问限制。 可以复制值以实现兼容性，在设备安装过程中直接修改值不会影响内部状态。

 

若要安全修改设备的软件密钥中其他注册表项的值，请遵循以下准则：

-   使用 [**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 和 [**SetupDiSetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw) 检索和设置标准或自定义属性。

    有关详细信息，请参阅 [访问设备驱动程序属性](accessing-device-driver-properties.md)。

-   仅设置操作系统未保留的设备属性。

    例如，要更改向用户显示的设备名称，请更改其 [**DEVPKEY_Device_FriendlyName**](./devpkey-device-friendlyname.md) 设备属性。

 

