---
title: 访问设备驱动程序属性
description: 访问设备驱动程序属性
ms.assetid: 433ad114-46aa-470b-b529-e6b6fb7f6bd7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1078a9fe4e6f69035f855fe0817f1f6e1e02eb97
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375711"
---
# <a name="accessing-device-driver-properties"></a>访问设备驱动程序属性


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)包含特征化设备驱动程序的设备驱动程序属性。 统一的设备属性模型使用[属性键](property-keys.md)来表示这些属性。

Windows Server 2003、 Windows XP 和 Windows 2000 还支持这些设备驱动程序属性中的大多数。 但是，这些早期版本的 Windows 不支持统一的设备属性模型属性键。 相反，这些版本的 Windows 使用以下机制来表示和访问相应的属性信息：

-   [访问有对应的注册表条目值的设备驱动程序属性](#accessing-device-driver-properties-that-have-corresponding-registry-en)
-   [使用 SetupDiGetDriverInstallParams 检索驱动程序级别](#using-setupdigetdriverinstallparams-to-retrieve-driver-rank)

为了保持与这些早期版本的 Windows、 Windows Vista 和更高版本的兼容性也支持这两种方式来访问设备接口的信息。 但是，应使用属性键来访问这些属性在 Windows Vista 和更高版本上。

系统定义的设备驱动程序属性的列表，请参阅[设备驱动程序属性](https://msdn.microsoft.com/library/windows/hardware/ff541205)。 属性的密钥标识符用于访问 Windows Vista 和更高版本上的属性按列出的设备驱动程序属性。 与属性键一起提供的信息包括可用于访问 Windows Server 2003、 Windows XP 和 Windows 2000 上的属性的相应系统定义的注册表条目值的名称。

有关如何使用属性键来访问在 Windows Vista 和更高版本上的设备驱动程序属性的信息，请参阅[访问设备实例属性 （Windows Vista 和更高版本）](accessing-device-instance-properties--windows-vista-and-later-.md)。

### <a href="" id="accessing-device-driver-properties-that-have-corresponding-registry-en"></a> 访问有对应的注册表条目值的设备驱动程序属性

若要访问 Windows Server 2003、 Windows XP 和 Windows 2000 上的设备驱动程序属性，请按照下列步骤：

1.  调用[ **SetupDiOpenDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552079)检索设备实例软件密钥的句柄。 提供以下参数值：

    -   设置*DeviceInfoSet*到包含要为其检索全球软件密钥的设备信息元素的设备信息集的句柄。
    -   设置*DeviceInfoData*指向的[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)结构，它表示要为其检索全球软件密钥的设备信息元素。
    -   设置*作用域*DICS_FLAG_GLOBAL 到。
    -   设置*HwProfile*为零。
    -   设置*KeyType* DIREG_DRV，为其配置**SetupDiOpenDevRegKey**检索设备实例软件密钥的句柄。
    -   设置*samDesired*到 REGSAM 类型化值，该值指定需要此密钥的访问权限。 对于所有访问设置*samDesired* KEY_ALL_ACCESS 到。

    如果在调用[ **SetupDiOpenDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552079)成功， **SetupDiOpenDevRegKey**返回请求的软件密钥的句柄。 如果函数调用失败， **SetupDiOpenDevRegKey**返回 INVALID_HANDLE_VALUE。 随后调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回最近记录的错误代码。

2.  提供对的调用中的句柄[RegQueryValueEx](https://go.microsoft.com/fwlink/p/?linkid=95398)或设置为[RegSetValueEx](https://go.microsoft.com/fwlink/p/?linkid=95399)以检索或设置相对应的注册表项值为设备实例驱动程序属性。

3.  调用[RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)函数之后不再需要访问密钥时关闭软件注册表项。

### <a href="" id="using-setupdigetdriverinstallparams-to-retrieve-driver-rank"></a> 使用 SetupDiGetDriverInstallParams 检索驱动程序级别

在 Windows Server 2003、 Windows XP 和 Windows 2000 上，可以检索的设备当前通过调用安装的驱动程序的秩[ **SetupDiGetDriverInstallParams**](https://msdn.microsoft.com/library/windows/hardware/ff551978)。 **SetupDiGetDriverInstallParams**检索到指针[ **SP_DRVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553290)中的输出参数，驱动程序的结构*DriverInstallParams*. **排名**检索 SP_DRVINSTALL_PARAMS 结构中的成员包含驱动程序级别。

 

 





