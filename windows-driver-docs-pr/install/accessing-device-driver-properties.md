---
title: 访问设备驱动程序属性
description: 访问设备驱动程序属性
ms.assetid: 433ad114-46aa-470b-b529-e6b6fb7f6bd7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a9dba2715eff99b80a29cc45c5752a945f6ff44
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732877"
---
# <a name="accessing-device-driver-properties"></a>访问设备驱动程序属性


在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 包括特征设备驱动程序的设备驱动程序属性。 统一设备属性模型使用 [属性键](property-keys.md) 来表示这些属性。

Windows Server 2003、Windows XP 和 Windows 2000 还支持这些设备驱动程序中的大多数属性。 但是，这些早期版本的 Windows 不支持统一设备属性模型的属性键。 相反，这些版本的 Windows 使用以下机制来表示和访问相应的属性信息：

-   [访问具有相应注册表项值的设备驱动程序属性](#accessing-device-driver-properties-that-have-corresponding-registry-en)
-   [使用 SetupDiGetDriverInstallParams 检索驱动程序级别](#using-setupdigetdriverinstallparams-to-retrieve-driver-rank)

为了保持与这些早期版本的 Windows 的兼容性，Windows Vista 及更高版本还支持通过这两种方式访问有关设备接口的信息。 但是，在 Windows Vista 和更高版本上，你应该使用属性键来访问这些属性。

有关系统定义的设备驱动程序属性的列表，请参阅 [设备驱动程序属性](/previous-versions/ff541205(v=vs.85))。 设备驱动程序属性由用于访问 Windows Vista 和更高版本上的属性的属性键标识符列出。 使用属性键提供的信息包括相应系统定义的注册表项值的名称，您可以使用这些值在 Windows Server 2003、Windows XP 和 Windows 2000 上访问该属性。

有关如何使用属性键访问 Windows Vista 和更高版本上的设备驱动程序属性的信息，请参阅 [ (Windows vista 和更高版本) 访问设备实例属性 ](accessing-device-instance-properties--windows-vista-and-later-.md)。

### <a name="accessing-device-driver-properties-that-have-corresponding-registry-entry-values"></a><a href="" id="accessing-device-driver-properties-that-have-corresponding-registry-en"></a> 访问具有相应注册表项值的设备驱动程序属性

若要在 Windows Server 2003、Windows XP 和 Windows 2000 上访问设备驱动程序属性，请执行以下步骤：

1.  调用 [**SetupDiOpenDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendevregkey) 可检索设备实例的软件密钥的句柄。 提供以下参数值：

    -   将 *DeviceInfoSet* 设置为设备信息集的句柄，其中包含要为其检索全局软件密钥的设备信息元素。
    -   将 *DeviceInfoData* 设置为指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构表示要为其检索全局软件密钥的设备信息元素。
    -   将 *作用域* 设置为 DICS_FLAG_GLOBAL。
    -   将 *hwprofile 中* 设置为零。
    -   将 *KeyType* 设置为 DIREG_DRV，它将 **SetupDiOpenDevRegKey** 配置为检索设备实例的软件密钥的句柄。
    -   将 *samDesired* 设置为 REGSAM 类型的值，该值指定此密钥所需的访问权限。 对于所有访问权限，请将 *samDesired* 设置为 KEY_ALL_ACCESS。

    如果对 [**SetupDiOpenDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendevregkey) 的调用成功，则 **SetupDiOpenDevRegKey** 将返回所请求软件密钥的句柄。 如果函数调用失败， **SetupDiOpenDevRegKey** 将返回 INVALID_HANDLE_VALUE。 对 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 的后续调用将返回最近记录的错误代码。

2.  在对 [RegQueryValueEx](/windows/win32/api/winreg/nf-winreg-regqueryvalueexa) 或 [RegSetValueEx](/windows/win32/api/winreg/nf-winreg-regsetvalueexa) 的调用中提供句柄，以检索或设置与设备实例驱动程序属性对应的注册表项值。

3.  调用 [RegCloseKey](/windows/win32/api/winreg/nf-winreg-regclosekey) 函数可在不再需要访问密钥后关闭软件注册表项。

### <a name="using-setupdigetdriverinstallparams-to-retrieve-driver-rank"></a><a href="" id="using-setupdigetdriverinstallparams-to-retrieve-driver-rank"></a> 使用 SetupDiGetDriverInstallParams 检索驱动程序级别

在 Windows Server 2003、Windows XP 和 Windows 2000 上，你可以通过调用 [**SetupDiGetDriverInstallParams**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdriverinstallparamsa)来检索当前为设备安装的驱动程序的排名。 **SetupDiGetDriverInstallParams**检索指向输出参数*DriverInstallParams*中驱动程序的[**SP_DRVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_drvinstall_params)结构的指针。 检索到的 SP_DRVINSTALL_PARAMS 结构的 **排名** 成员包含驱动程序级别。

