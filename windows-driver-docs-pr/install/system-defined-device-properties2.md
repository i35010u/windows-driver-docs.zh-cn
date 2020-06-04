---
title: 系统定义的设备属性
description: 系统定义的设备属性
ms.assetid: 9d823a9f-0802-4e92-bf94-abb5b0e7b9ee
keywords:
- 设备属性 WDK 设备安装，系统定义
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca583ca5242add42be6d73c56321d1d2622396b4
ms.sourcegitcommit: a386cf5ac5a157dfe1041e7c23b6e70a33ca2704
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330059"
---
# <a name="system-defined-device-properties"></a>系统定义的设备属性


在 Windows Vista 和更高版本的 Windows 中，[统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md)支持定义设备实例、[设备安装程序类](device-setup-classes.md)、[设备接口类](device-interface-classes.md)和设备接口的配置或操作的系统定义属性。 每个属性都由一个[属性键](property-keys.md)表示，该属性键是一个 GUID 值，用于标识属性类别和属性标识符。 系统定义的属性键类别只保留供系统使用。

下面是在*Devpkey*中定义的系统定义的设备属性键：

-   DEVPKEY_NAME 属性键，它表示组件的名称。 使用 DEVPKEY_NAME 属性的值将组件识别为最终用户。 Windows 支持[**设备实例**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-name--device-instance-)、[**设备安装程序类**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-name--device-setup-class-)和[**设备接口**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-name--device-interface-)的 DEVPKEY_NAME 属性。

-   属性键，表示与[SPDRP_Xxx 标识符对应的设备实例属性](https://docs.microsoft.com/previous-versions/ff541334(v=vs.85))。 （SPDRP_*Xxx*标识符在*setupapi.log*中定义。）

-   表示没有相应 SPDRP_*Xxx*标识符的设备实例属性的属性键。 其中包括：

    [设备状态和问题属性](https://docs.microsoft.com/windows-hardware/drivers/install/retrieving-the-status-and-problem-code-for-a-device-instance)

    [设备关系属性](https://docs.microsoft.com/previous-versions/ff541498(v=vs.85))，包括父设备、子设备和同级设备

    [设备驱动程序属性](https://docs.microsoft.com/previous-versions/ff541205(v=vs.85))

    [设备驱动程序包属性](https://docs.microsoft.com/previous-versions/ff541200(v=vs.85))

    [其他设备属性](https://docs.microsoft.com/previous-versions/ff549289(v=vs.85))

-   属性键，表示与 SPCRP_Xxx 标识符对应的[设备安装程序类属性](https://docs.microsoft.com/previous-versions/ff542239(v=vs.85))。 （SPCRP_Xxx 在*setupapi.log*中定义的标识符。）

-   表示设备安装程序类属性的属性键，这些属性没有对应的 SPCRP_Xxx 标识符。

-   表示[设备接口类属性](https://docs.microsoft.com/previous-versions/ff541406(v=vs.85))的属性键。

-   表示[设备接口属性](https://docs.microsoft.com/previous-versions/ff541409(v=vs.85))的属性键。

有关如何创建自定义设备属性的信息，请参阅[创建自定义设备属性](creating-custom-device-properties.md)。

 

 





