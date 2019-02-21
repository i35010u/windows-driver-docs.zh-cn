---
title: 访问自定义设备属性
description: 访问自定义设备属性
ms.assetid: 81170fd5-f1fb-4a06-a651-4651fc894070
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b49c22d6241e2fa41508d7c54be80f0c84cf077
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554804"
---
# <a name="accessing-custom-device-properties"></a>访问自定义设备属性


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)支持使用[属性键](property-keys.md)创建和访问自定义设备属性。 有关详细信息，请参阅[创建自定义设备属性](creating-custom-device-properties.md)。

在 Windows Server 2003、 Windows XP 和 Windows 2000 上，可以创建自定义注册表条目与设备相关组件的系统提供的注册表项下的值。 以下列表包含要调用的每种类型的设备组件以打开相应的系统提供的注册表项的安装程序 Api 函数。 在打开的系统定义的注册表项后，应用程序和安装程序可以调用要修改自定义注册表条目值，打开注册表项下的基于 Windows 的注册表函数。

-   设备实例硬件属性的自定义注册表项值应位于设备实例的硬件注册表项下。 调用[ **SetupDiOpenDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552079) ，并提供在 DIREG_DEV*标志*参数，检索设备实例的硬件密钥的句柄。 可以通过调用检索设备实例设置硬件注册表项下的自定义注册表项值[ **SetupDiGetCustomDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551099)函数。

-   设备实例软件属性的自定义注册表项值应位于设备实例的软件注册表项下。 调用**SetupDiOpenDevRegKey** ，并提供在 DIREG_DRV*标志*参数，检索设备实例软件密钥的句柄。

-   自定义注册表项值[设备安装程序类属性](accessing-device-setup-class-properties.md)应位于设备安装程序类注册表项下。 调用[ **SetupDiOpenClassRegKeyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552067) ，并提供在 DIOCR_INSTALLER*标志*参数，检索设备安装程序类的注册表项的句柄。

-   设备接口类属性的自定义注册表项值应位于设备接口类注册表项下。 调用**SetupDiOpenClassRegKeyEx** ，并提供在 DIOCR_INTERFACE*标志*参数，检索设备接口类的注册表项的句柄。

-   设备接口属性的自定义注册表项值应位于设备接口注册表项下。 调用[ **SetupDiOpenDeviceInterfaceRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552075)检索设备接口类的注册表项的句柄。

检索的句柄注册表项后，提供对的调用中的句柄[RegQueryValueEx](https://go.microsoft.com/fwlink/p/?linkid=95398)或[RegSetValueEx](https://go.microsoft.com/fwlink/p/?linkid=95399)以检索或设置相对应的自定义注册表项值为自定义设备属性。

调用[RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)函数之后不再需要访问的注册表项时关闭注册表项。

 

 





