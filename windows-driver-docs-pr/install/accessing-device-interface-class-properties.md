---
title: 访问设备接口类属性
description: 访问设备接口类属性
ms.assetid: c9efe273-dc66-4585-8ab5-3842df1c95df
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6f177b9ca6cb6543bc7109658aef2eac83e01f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383049"
---
# <a name="accessing-device-interface-class-properties"></a>访问设备接口类属性


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)包含设备接口类属性描述设备接口类的特征。 统一的设备属性模型使用[属性键](property-keys.md)来表示这些属性。

Windows Server 2003、 Windows XP 和 Windows 2000 还支持大部分设备接口类属性。 但是，这些早期版本的 Windows 不支持统一的设备属性模型属性键。 相反，可以表示，并使用以下方法访问这些版本的 Windows 上的相应属性信息：

-   [访问设备接口类的默认接口](#accessing-the-default-interface-for-a-device-interface-class)

-   [访问设备具有接口类注册表项下的注册表条目值的接口类属性](#accessing-device-interface-class-properties-that-have-registry-entry-v)

为了保持与这些早期版本的 Windows、 Windows Vista 和更高版本的兼容性也支持这两种方式来访问设备接口的信息。 但是，应使用属性键来访问这些属性在 Windows Vista 和更高版本。

系统定义的设备接口的类属性的列表，请参阅[设备接口类属性](https://docs.microsoft.com/previous-versions/ff541406(v=vs.85))。 [设备安装程序类属性](accessing-device-setup-class-properties.md)列出的属性的密钥标识符用于访问在 Windows Vista 和更高版本中的属性。 与属性键一起提供的信息还包括可用于访问 Windows Server 2003、 Windows XP 和 Windows 2000 上的属性的相应注册表项值。

有关如何使用属性键来访问在 Windows Vista 和更高版本的设备安装程序类属性的信息，请参阅[访问设备类属性 （Windows Vista 和更高版本）](accessing-device-class-properties--windows-vista-and-later-.md)。

### <a href="" id="accessing-the-default-interface-for-a-device-interface-class"></a> 访问设备接口类的默认接口

若要检索的设备接口类的默认接口，请调用[ **SetupDiGetClassDevs** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)并提供以下参数值：

-   设置*ClassGuid*到表示要为其检索默认接口的设备接口类的 GUID。

-   设置 * 枚举器  **NULL** 。

-   设置*hwndParent*到**NULL**。

-   设置*标志*到 (DIGCF_DEVICEINTERFACE |DIGCF_DEFAULT)。

此调用将返回包含设备信息元素的设备信息集。 返回的设备信息元素表示为指定的设备接口类支持的默认接口的设备。

若要设置设备接口类的默认接口，请调用[ **SetupDiSetDeviceInterfaceDefault** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacedefault) ，并提供以下参数值：

-   设置*DeviceInfoSet*到设备的信息集，其中包含要为设备接口类的默认设置的设备接口的句柄。

-   设置*DeviceInterfaceData*指向的[ **SP_DEVICE_INTERFACE_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_data)结构，它指定在设备接口*DeviceInfoSet*.

### <a href="" id="accessing-device-interface-class-properties-that-have-registry-entry-v"></a> 访问设备具有接口类注册表项下的注册表条目值的接口类属性

若要访问的设备接口类都具有相应接口类注册表项下的注册表条目值的属性，请按照下列步骤：

1.  调用[ **SetupDiOpenClassRegKeyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)函数打开接口类注册表项，并提供以下参数值：

    -   设置*ClassGuid*为指向标识设备接口的类的请求的类注册表项的 GUID。
    -   设置*samDesired*到 REGSAM 类型化值，该值指定所需的访问权限。
    -   设置*标志*DIOCR_INTERFACE 到。
    -   设置*MachineName*为指向包含要打开请求的类注册表项的计算机的名称的以 NULL 结尾的字符串。 如果计算机是本地计算机，设置*MachineName*到**NULL**。
    -   设置*保留*到**NULL**。

    如果此调用[ **SetupDiOpenClassRegKeyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)成功， **SetupDiOpenClassRegKeyEx**返回请求的句柄。 如果函数调用失败， **SetupDiOpenClassRegKeyEx**将返回 INVALID_HANDLE_VALUE 和调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回的记录的错误代码。

2.  提供对的调用中检索到的句柄[RegQueryValueEx](https://go.microsoft.com/fwlink/p/?linkid=95398)并[RegSetValueEx](https://go.microsoft.com/fwlink/p/?linkid=95399)以检索或设置相对应的注册表项值为设备接口的类属性。

3.  调用[RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)函数之后不再需要访问密钥时关闭类注册表项。

有关如何安装和使用设备接口的信息，请参阅[设备接口类](device-interface-classes.md)并[ **INF AddInterface 指令**](inf-addinterface-directive.md)。

 

 





