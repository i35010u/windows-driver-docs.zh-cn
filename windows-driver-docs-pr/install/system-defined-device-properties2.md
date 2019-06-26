---
title: 系统定义的设备属性
description: 系统定义的设备属性
ms.assetid: 9d823a9f-0802-4e92-bf94-abb5b0e7b9ee
keywords:
- 系统定义的设备属性 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfa4ae50e99c87c9bbffc4b79125d88f8de92b28
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385864"
---
# <a name="system-defined-device-properties"></a>系统定义的设备属性


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)支持特征化的配置或操作的设备实例的系统定义属性[设备安装程序类](device-setup-classes.md)，[设备接口类](device-interface-classes.md)，和设备接口。 每个属性表示由[属性键](property-keys.md)，这是用于标识的属性类别和属性标识符的 GUID 值。 仅供系统使用保留的系统定义的属性键的类别。

在中定义以下系统定义的设备属性键*Devpkey.h*:

-   DEVPKEY_NAME 属性键，它表示组件的名称。 使用 DEVPKEY_NAME 属性的值来识别为其最终用户的组件。 Windows 支持的 DEVPKEY_NAME 属性[**设备实例**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-name--device-instance-)， [**设备安装程序类**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-name--device-setup-class-)，和[ **设备接口**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-name--device-interface-)。

-   属性键，分别代表[设备实例属性对应于 SPDRP_Xxx 标识符](https://docs.microsoft.com/previous-versions/ff541334(v=vs.85))。 (SPDRP_*Xxx*中定义的标识符*Setupapi.h*。)

-   表示设备的属性项实例属性不具有相应 SPDRP_*Xxx*标识符。 这包括以下内容：

    [设备状态和问题属性](https://docs.microsoft.com/previous-versions/ff542254(v=vs.85))

    [设备的关系属性](https://docs.microsoft.com/previous-versions/ff541498(v=vs.85))，包括父设备、 子设备和同级设备

    [设备驱动程序属性](https://docs.microsoft.com/previous-versions/ff541205(v=vs.85))

    [设备驱动程序包属性](https://docs.microsoft.com/previous-versions/ff541200(v=vs.85))

    [杂项其他设备属性](https://docs.microsoft.com/previous-versions/ff549289(v=vs.85))

-   属性键，分别代表[设备安装程序类属性](https://docs.microsoft.com/previous-versions/ff542239(v=vs.85))SPCRP_Xxx 标识符相对应。 (在中定义的 SPCRP_Xxx 标识符*Setupapi.h*。)

-   表示不具有相应 SPCRP_Xxx 标识符的设备安装程序类属性的属性键。

-   属性键，分别代表[设备接口类属性](https://docs.microsoft.com/previous-versions/ff541406(v=vs.85))。

-   属性键，分别代表[设备接口属性](https://docs.microsoft.com/previous-versions/ff541409(v=vs.85))。

有关如何创建自定义设备属性的信息，请参阅[创建自定义设备属性](creating-custom-device-properties.md)。

 

 





