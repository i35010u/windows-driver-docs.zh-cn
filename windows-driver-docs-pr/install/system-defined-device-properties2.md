---
title: 系统定义的设备属性
description: 系统定义的设备属性
ms.assetid: 9d823a9f-0802-4e92-bf94-abb5b0e7b9ee
keywords:
- 设备属性 WDK 设备安装，系统定义
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 505cdb3cb6741e7139d8fd6bb2a38a7ca4c1c4e6
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096213"
---
# <a name="system-defined-device-properties"></a>系统定义的设备属性


在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 支持定义设备实例、 [设备安装程序类](./overview-of-device-setup-classes.md)、 [设备接口类](./overview-of-device-interface-classes.md)和设备接口的配置或操作的系统定义属性。 每个属性都由一个 [属性键](property-keys.md)表示，该属性键是一个 GUID 值，用于标识属性类别和属性标识符。 系统定义的属性键类别只保留供系统使用。

下面是在 *Devpkey*中定义的系统定义的设备属性键：

-   DEVPKEY_NAME 属性键，它表示组件的名称。 使用 DEVPKEY_NAME 属性的值将组件识别为最终用户。 Windows 支持 [**设备实例**](./devpkey-name--device-instance-.md)、 [**设备安装程序类**](./devpkey-name--device-setup-class-.md)和 [**设备接口**](./devpkey-name--device-interface-.md)的 DEVPKEY_NAME 属性。

-   属性键，表示与 [SPDRP_Xxx 标识符对应的设备实例属性](/previous-versions/ff541334(v=vs.85))。  (在*setupapi.log*中定义 SPDRP_*Xxx*标识符。 ) 

-   表示没有相应 SPDRP_*Xxx* 标识符的设备实例属性的属性键。 这包括：

    [设备状态和问题属性](./retrieving-the-status-and-problem-code-for-a-device-instance.md)

    [设备关系属性](/previous-versions/ff541498(v=vs.85))，包括父设备、子设备和同级设备

    [设备驱动程序属性](/previous-versions/ff541205(v=vs.85))

    [设备驱动程序包属性](/previous-versions/ff541200(v=vs.85))

    [其他设备属性](/previous-versions/ff549289(v=vs.85))

-   属性键，表示与 SPCRP_Xxx 标识符对应的 [设备安装程序类属性](/previous-versions/ff542239(v=vs.85)) 。  (在 *setupapi.log*中定义 SPCRP_Xxx 标识符。 ) 

-   表示设备安装程序类属性的属性键，这些属性没有对应的 SPCRP_Xxx 标识符。

-   表示 [设备接口类属性](/previous-versions/ff541406(v=vs.85))的属性键。

-   表示 [设备接口属性](/previous-versions/ff541409(v=vs.85))的属性键。

有关如何创建自定义设备属性的信息，请参阅 [创建自定义设备属性](creating-custom-device-properties.md)。

 

