---
title: 在 Windows Vista 之前访问设备接口属性
description: 在 Windows Vista 之前访问设备接口属性
ms.assetid: 48b47d01-ec07-49ca-a03c-c4c387dcfb19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07efeec034abf92bdd3eae2d4543a90119d3bfbe
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097161"
---
# <a name="accessing-device-interface-properties-before-windows-vista"></a>在 Windows Vista 之前访问设备接口属性


在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 包括用于描述设备接口特征的设备接口属性。 统一设备属性模型使用 [属性键](property-keys.md) 来表示这些属性。

Windows Server 2003、Windows XP 和 Windows 2000 支持其中大多数设备接口类属性。 但是，这些早期版本的 Windows 不支持统一设备属性模型的属性键。 相反，这些版本的 Windows 使用以下机制来表示和访问设备接口属性：

-   [访问具有相应注册表项值的设备接口属性](#accessing-device-interface-properties-that-have-corresponding-registry)

-   [使用 SetupDiEnumDeviceInterfaces 检索有关设备接口的信息](#using-setupdienumdeviceinterfaces-to-retrieve-information-about-a-devi)。

为了保持与这些早期版本的 Windows 的兼容性，Windows Vista 及更高版本还支持通过这两种方式访问有关设备接口的信息。 但是，在 Windows Vista 和更高版本中，你应该使用属性键来访问这些属性。

有关系统定义的设备接口类属性的列表，请参阅 [设备接口属性](/previous-versions/ff541409(v=vs.85))。 设备接口类属性按其相应的属性键列出，您可以使用这些属性键访问 Windows Vista 和更高版本中的属性。 使用属性键提供的信息包括可用于访问 Windows Server 2003、Windows XP 和 Windows 2000 上的属性的相应注册表项值（如果有）。

有关如何使用属性键访问 Windows Vista 和更高版本中的设备安装程序类属性的信息，请参阅 [ (Windows vista 和更高版本) 访问设备接口属性 ](accessing-device-interface-properties--windows-vista-and-later-.md)。

有关如何安装和使用设备接口的信息，请参阅 [设备接口类](./overview-of-device-interface-classes.md) 和 [**INF AddInterface 指令**](inf-addinterface-directive.md)。

### <a name="accessing-device-interface-properties-that-have-corresponding-registry-entry-values"></a><a href="" id="accessing-device-interface-properties-that-have-corresponding-registry"></a> 访问具有相应注册表项值的设备接口属性

若要使用 Windows Server 2003、Windows XP 和 Windows 2000 上的注册表项值访问设备接口属性，请先调用 [**SetupDiOpenDeviceInterfaceRegKey**](/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey)并提供以下参数：

-   将 *DeviceInfoSet* 设置为指向包含设备接口的设备信息集的指针。

-   将 *DeviceInterfaceData* 设置为指向标识设备接口的 [**SP_DEVICE_INTERFACE_DATA**](/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_data) 结构的指针。

-   将 *保留* 设置为零。

-   将 *samDesired* 设置为 REGSAM 类型的值，该值指定所需的访问权限。

如果对 [**SetupDiOpenDeviceInterfaceRegKey**](/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey) 的此调用成功，则 **SetupDiOpenDeviceInterfaceRegKey** 将返回请求的句柄。 如果函数调用失败，则 **SetupDiOpenDeviceInterfaceRegKey** 将返回 INVALID_HANDLE_VALUE 并且对 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) 的调用将返回记录的错误代码。

检索设备接口注册表项的句柄之后，在对 [RegQueryValueEx](https://go.microsoft.com/fwlink/p/?linkid=95398) 或 [RegSetValueEx](https://go.microsoft.com/fwlink/p/?linkid=95399) 的调用中提供句柄，以检索或设置与设备接口属性相对应的注册表项值。

调用 [RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543) 函数可在不再需要访问密钥后关闭类注册表项。

### <a name="using-setupdienumdeviceinterfaces-to-retrieve-information-about-a-device-interface"></a><a href="" id="using-setupdienumdeviceinterfaces-to-retrieve-information-about-a-devi"></a> 使用 SetupDiEnumDeviceInterfaces 检索有关设备接口的信息

若要在 Windows Server 2003、Windows XP 和 Windows 2000 上检索有关设备接口的信息，另一种方法是通过调用 [**SetupDiEnumDeviceInterfaces**](/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces) 来检索接口的 [**SP_DEVICE_INTERFACE_DATA**](/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_data) 结构。 SP_DEVICE_INTERFACE_DATA 结构包含以下信息：

-   **Flags**成员指示设备接口是否处于活动状态或已删除，以及设备是否为接口类的默认接口。

-   **InterfaceClassGuild**成员标识接口类 GUID。

 

