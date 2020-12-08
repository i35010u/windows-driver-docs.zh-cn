---
title: 访问设备接口类属性
description: 访问设备接口类属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ad7ec97c7d0ed8ba386de152e8c3e18ee9babdd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826259"
---
# <a name="accessing-device-interface-class-properties"></a>访问设备接口类属性


在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 包括用于描述设备接口类的特征的设备接口类属性。 统一设备属性模型使用 [属性键](property-keys.md) 来表示这些属性。

Windows Server 2003、Windows XP 和 Windows 2000 还支持其中的大多数设备接口类属性。 但是，这些早期版本的 Windows 不支持统一设备属性模型的属性键。 相反，你可以使用以下方法来表示和访问这些版本的 Windows 上的相应属性信息：

-   [访问设备接口类的默认接口](#accessing-the-default-interface-for-a-device-interface-class)

-   [访问具有 Interface 类注册表项下的注册表项值的设备接口类属性](#accessing-device-interface-class-properties-that-have-registry-entry-v)

为了保持与这些早期版本的 Windows 的兼容性，Windows Vista 及更高版本还支持通过这两种方式访问有关设备接口的信息。 但是，在 Windows Vista 和更高版本中，你应该使用属性键来访问这些属性。

有关系统定义的设备接口类属性的列表，请参阅 [设备接口类属性](/previous-versions/ff541406(v=vs.85))。 [设备安装程序类属性](accessing-device-setup-class-properties.md)由用于访问 Windows Vista 和更高版本中的属性的属性键标识符列出。 使用属性键提供的信息还包含相应的注册表项值，你可以使用这些值来访问 Windows Server 2003、Windows XP 和 Windows 2000 上的属性。

有关如何使用属性键访问 Windows Vista 和更高版本中的设备安装程序类属性的信息，请参阅 [访问设备类属性 (Windows vista 和更高版本) ](accessing-device-class-properties--windows-vista-and-later-.md)。

### <a name="accessing-the-default-interface-for-a-device-interface-class"></a><a href="" id="accessing-the-default-interface-for-a-device-interface-class"></a> 访问设备接口类的默认接口

若要检索设备接口类的默认接口，请调用 [**SetupDiGetClassDevs**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsw) 并提供以下参数值：

-   将 *ClassGuid* 设置为表示要为其检索默认接口的设备接口类的 GUID。

-   Set * 枚举器 ***NULL**。

-   将 *hwndParent* 设置为 **NULL**。

-   将 *标志* 设置为 (DIGCF_DEVICEINTERFACE |DIGCF_DEFAULT) 。

此调用将返回包含设备信息元素的设备信息集。 返回的设备信息元素表示支持指定设备接口类的默认接口的设备。

若要设置设备接口类的默认接口，请调用 [**SetupDiSetDeviceInterfaceDefault**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdeviceinterfacedefault) 并提供以下参数值：

-   将 *DeviceInfoSet* 设置为设备信息集的句柄，其中包含要设置为设备接口类的默认值的设备接口。

-   将 *DeviceInterfaceData* 设置为指向指定 *DeviceInfoSet* 中的设备接口的 [**SP_DEVICE_INTERFACE_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_device_interface_data)结构的指针。

### <a name="accessing-device-interface-class-properties-that-have-registry-entry-values-under-the-interface-class-registry-key"></a><a href="" id="accessing-device-interface-class-properties-that-have-registry-entry-v"></a> 访问具有 Interface 类注册表项下的注册表项值的设备接口类属性

若要访问具有 interface 类注册表项下的相应注册表项值的设备接口类的属性，请执行以下步骤：

1.  调用 [**SetupDiOpenClassRegKeyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa) 函数以打开接口类注册表项，并提供以下参数值：

    -   将 *ClassGuid* 设置为一个指向 GUID 的指针，该 GUID 标识所请求的类注册表项的设备接口类。
    -   将 *samDesired* 设置为 REGSAM 类型的值，该值指定所需的访问权限。
    -   将 *标志* 设置为 DIOCR_INTERFACE。
    -   将 *MachineName* 设置为指向以 NULL 结尾的字符串的指针，该字符串包含要在其上打开请求的类注册表项的计算机的名称。 如果计算机是本地计算机，请将 *MachineName* 设置为 **NULL**。
    -   将 *保留* 设置为 **NULL**。

    如果对 [**SetupDiOpenClassRegKeyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa) 的此调用成功，则 **SetupDiOpenClassRegKeyEx** 将返回请求的句柄。 如果函数调用失败，则 **SetupDiOpenClassRegKeyEx** 将返回 INVALID_HANDLE_VALUE 并且对 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 的调用将返回记录的错误代码。

2.  在对 [RegQueryValueEx](/windows/win32/api/winreg/nf-winreg-regqueryvalueexa) 和 [RegSetValueEx](/windows/win32/api/winreg/nf-winreg-regsetvalueexa) 的调用中提供检索到的句柄，以检索或设置与设备接口类属性相对应的注册表项值。

3.  调用 [RegCloseKey](/windows/win32/api/winreg/nf-winreg-regclosekey) 函数可在不再需要访问密钥后关闭类注册表项。

有关如何安装和使用设备接口的信息，请参阅 [设备接口类](./overview-of-device-interface-classes.md) 和 [**INF AddInterface 指令**](inf-addinterface-directive.md)。

