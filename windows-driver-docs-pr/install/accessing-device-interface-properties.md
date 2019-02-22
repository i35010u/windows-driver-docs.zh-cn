---
title: 访问 Windows Vista 之前的设备接口属性
description: 访问 Windows Vista 之前的设备接口属性
ms.assetid: 48b47d01-ec07-49ca-a03c-c4c387dcfb19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dcc5dead79529f0fe8dacc4e40fdc7a4e56516c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541919"
---
# <a name="accessing-device-interface-properties-before-windows-vista"></a>访问 Windows Vista 之前的设备接口属性


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)包含设备特征化设备接口的接口属性。 统一的设备属性模型使用[属性键](property-keys.md)来表示这些属性。

Windows Server 2003、 Windows XP 和 Windows 2000 支持大部分设备接口类属性。 但是，这些早期版本的 Windows 不支持统一的设备属性模型属性键。 相反，这些版本的 Windows 使用以下机制来表示和访问设备接口属性：

-   [访问有对应的注册表条目值的设备接口属性](#accessing-device-interface-properties-that-have-corresponding-registry)

-   [使用 SetupDiEnumDeviceInterfaces 检索设备接口的信息](#using-setupdienumdeviceinterfaces-to-retrieve-information-about-a-devi)。

为了保持与这些早期版本的 Windows、 Windows Vista 和更高版本的兼容性也支持这两种方式来访问设备接口的信息。 但是，应使用属性键来访问这些属性在 Windows Vista 和更高版本。

系统定义的设备接口的类属性的列表，请参阅[设备接口属性](https://msdn.microsoft.com/library/windows/hardware/ff541409)。 通过用于访问在 Windows Vista 和更高版本中的属性及其对应的属性项列出设备接口的类属性。 与属性键一起提供的信息包括相应的注册表条目值，如果有，可用于访问 Windows Server 2003、 Windows XP 和 Windows 2000 上的属性。

有关如何使用属性键来访问在 Windows Vista 和更高版本的设备安装程序类属性的信息，请参阅[访问设备接口属性 （Windows Vista 和更高版本）](accessing-device-interface-properties--windows-vista-and-later-.md)。

有关如何安装和使用设备接口的信息，请参阅[设备接口类](device-interface-classes.md)并[ **INF AddInterface 指令**](inf-addinterface-directive.md)。

### <a href="" id="accessing-device-interface-properties-that-have-corresponding-registry"></a> 访问有对应的注册表条目值的设备接口属性

通过在 Windows Server 2003、 Windows XP 和 Windows 2000 中，首次调用使用注册表条目值的访问设备接口属性[ **SetupDiOpenDeviceInterfaceRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552075)并提供以下参数：

-   设置*DeviceInfoSet*为指向包含设备接口的设备信息集。

-   设置*DeviceInterfaceData*指向的[ **SP_DEVICE_INTERFACE_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552342)标识设备接口的结构。

-   设置*保留*为零。

-   设置*samDesired*到 REGSAM 类型化值，该值指定所需的访问权限。

如果此调用[ **SetupDiOpenDeviceInterfaceRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552075)成功， **SetupDiOpenDeviceInterfaceRegKey**返回请求的句柄。 如果函数调用失败， **SetupDiOpenDeviceInterfaceRegKey**将返回 INVALID_HANDLE_VALUE 和调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回的记录的错误代码。

检索设备接口注册表项的句柄后，提供对的调用中的句柄[RegQueryValueEx](https://go.microsoft.com/fwlink/p/?linkid=95398)或[RegSetValueEx](https://go.microsoft.com/fwlink/p/?linkid=95399)要检索或设置对应的注册表项值设备接口属性。

调用[RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)函数之后不再需要访问密钥时关闭类注册表项。

### <a href="" id="using-setupdienumdeviceinterfaces-to-retrieve-information-about-a-devi"></a> 使用 SetupDiEnumDeviceInterfaces 检索设备接口的信息

另一种方法来检索有关设备接口在 Windows Server 2003、 Windows XP 和 Windows 2000 上的信息是通过调用[ **SetupDiEnumDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff551015)检索[ **SP_DEVICE_INTERFACE_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552342)结构接口。 SP_DEVICE_INTERFACE_DATA 结构包含以下信息：

-   **标志**成员指示设备接口处于活动状态还是将其删除，以及设备是否为接口类的默认接口。

-   **InterfaceClassGuild**成员标识接口的类 GUID。

 

 





