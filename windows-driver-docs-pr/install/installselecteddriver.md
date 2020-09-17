---
title: InstallSelectedDriver 函数
description: InstallSelectedDriver 函数将在所选设备上安装所选的驱动程序。
ms.assetid: 8a27f4bb-6d1e-4fe8-810f-23513418254d
keywords:
- InstallSelectedDriver 函数设备和驱动程序安装
topic_type:
- apiref
api_name:
- InstallSelectedDriver
api_location:
- Newdev.dll
api_type:
- DllExport
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 16c4bd9aee5a6971e3e8ab05e624239703093d7f
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714902"
---
# <a name="installselecteddriver-function"></a>InstallSelectedDriver 函数


不推荐使用 **InstallSelectedDriver** 函数。 对于 Windows Vista 和更高版本，请改用 [**DiInstallDevice**](/windows/win32/api/newdev/nf-newdev-diinstalldevice) 。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
BOOL WINAPI InstallSelectedDriver(
  _In_  HWND     hwndParent,
  _In_  HDEVINFO DeviceInfoSet,
  _In_  LPCTSTR  Reserved,
  _In_  BOOL     Backup,
  _Out_ PDWORD   bReboot
);
```

<a name="parameters"></a>参数
----------

*hwndParent* \[中\]  
顶级窗口的句柄， **InstallSelectedDriver** 函数使用该句柄显示与安装驱动程序相关联的用户界面组件。

*DeviceInfoSet* \[中\]  
[设备信息集](./device-information-sets.md)的句柄，其中包含表示所选设备和设备的所选驱动程序的设备信息元素。 有关如何为设备选择设备和驱动程序的详细信息，请参阅以下 " **备注** " 部分。

*保留* \[中\]  
此参数必须设置为 **NULL**。

*备份* \[中\]  
一个 BOOL 类型的值，它确定在函数安装所选设备的驱动程序之前， **InstallSelectedDriver** 是否备份所选设备的当前安装的驱动程序。 如果备份当前安装的驱动程序，并且用户遇到新的驱动程序问题，则用户可以将新驱动程序的安装回滚到备份的驱动程序中。 如果当前安装的驱动程序未备份，则用户无法将新驱动程序的安装回滚到以前安装的驱动程序。 如果 *备份* 设置为 **TRUE**，则 **InstallSelectedDriver** 将备份当前安装的驱动程序;否则，此函数不会备份当前安装的驱动程序。 有关驱动程序备份的详细信息，请参阅 **DiRollbackDriver**。

*bReboot* \[弄\]  
指向 DWORD 类型的变量的指针， **InstallSelectedDriver** 设置以指示是否需要重新启动系统才能完成安装。 如果将变量设置为 DI \_ NEEDREBOOT，则需要重新启动系统; 否则，不需要重新启动系统。 调用方负责重新启动系统。

<a name="return-value"></a>返回值
------------

如果选定的驱动程序安装在所选设备上，则**InstallSelectedDriver**返回**TRUE** ;否则，该函数将返回**FALSE** ，并通过调用**GetLastError**来检索记录的错误。

其他 **可能返回的其他** 错误值如下：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回代码</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>NO_ERROR</strong></td>
<td align="left"><p>所选的驱动程序比设备上以前安装的驱动程序更匹配。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ERROR_IN_WOW64</strong></td>
<td align="left"><p>调用应用程序是一个32位应用程序，该应用程序尝试在64位环境中执行，这是不允许的。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/install/device-installations-on-64-bit-systems" data-raw-source="[Installing Devices on 64-Bit Systems](./device-installations-on-64-bit-systems.md)">在64位系统上安装设备</a>。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

若要访问 **InstallSelectedDriver**，请调用 **LoadLibrary** 以加载 *Newdev.dll* ，然后调用 **GetProcAddress** 以获取指向 **InstallSelectedDriver**的函数指针。

仅当需要在特定设备上安装特定驱动程序时，才应调用 **InstallSelectedDriver** 。

**重要提示**   对于 Windows Vista 和更高版本的 Windows，请调用[**DiInstallDevice**](/windows/win32/api/newdev/nf-newdev-diinstalldevice)而不是**InstallSelectedDriver**来执行此类操作。

 

除了需要在特定设备上安装特定驱动程序的特殊应用程序外，安装应用程序应安装与设备最匹配的驱动程序。 若要安装最符合设备的驱动程序，请调用 [**DiInstallDriver**](/windows/win32/api/newdev/nf-newdev-diinstalldrivera) 或 [**UpdateDriverForPlugAndPlayDevices**](/windows/win32/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)。 若要详细了解在设备上安装驱动程序所要调用的函数的详细信息，请参阅 [Setupapi.log 函数，可简化驱动程序的安装](./functions-that-simplify-driver-installation.md)。

在调用 **InstallSelectedDriver**之前，调用方必须获取包含设备的设备信息集，选择设备集中的设备，然后选择设备驱动程序。

若要创建包含设备的设备信息集，请执行以下操作之一：

-   调用 [**SetupDiGetClassDevs**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsw) 检索包含设备的设备信息集，然后调用 [**SetupDiEnumDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinfo) 来枚举设备信息集中的设备。 在每次调用时， **SetupDiEnumDeviceInfo** 将 \_ 返回 \_ 表示设备信息集中的枚举设备的 SP lnk-devinfo 数据结构。 若要获取有关枚举设备的特定信息，请调用[**SetupDiGetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya) ，并提供 \_ SETUPDIENUMDEVICEINFO 返回的 SP lnk-devinfo \_ 数据**SetupDiEnumDeviceInfo**结构。

    - 或 -

-   调用 [**SetupDiOpenDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendeviceinfoa) ，将具有已知设备实例 ID 的设备添加到设备信息集。 **SetupDiOpenDeviceInfo** 返回 [**SP \_ lnk-devinfo \_ 数据**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构，该结构表示设备信息集中的设备。

获取设备的 SP \_ Lnk-devinfo \_ 数据结构后，调用 [**SetupDiSetSelectedDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdisetselecteddevice) 来选择设备信息集中的设备。

若要检索设备的驱动程序，请调用 [**SetupDiBuildDriverInfoList**](/windows/win32/api/setupapi/nf-setupapi-setupdibuilddriverinfolist) 来构建设备的兼容驱动程序列表，然后调用 [**SetupDiEnumDriverInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdriverinfoa) 来枚举设备的驱动程序列表中的元素。 对于每个枚举的**SetupDiEnumDriverInfo**驱动程序，SetupDiEnumDriverInfo \_ 检索 \_ 表示驱动程序的 SP DRVINFO 数据结构。 可以调用[**SetupDiGetDriverInfoDetail**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdriverinfodetaila)来检索有关枚举的驱动程序的其他详细信息。

\_ \_ 为驱动程序获取 SP DRVINFO 数据结构后，调用[**SetupDiSetSelectedDriver**](/windows/win32/api/setupapi/nf-setupapi-setupdisetselecteddrivera)选择设备驱动程序。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面型</td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Microsoft Windows 2000 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">无 (在公共头文件中未定义 <strong>InstallSelectedDriver</strong> 函数。 有关详细信息，请参阅<strong>备注</strong>部分。 )</td>
</tr>
<tr class="even">
<td align="left"><p>库</p></td>
<td align="left">Newdev</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">Newdev.dll</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DiInstallDevice**](/windows/win32/api/newdev/nf-newdev-diinstalldevice)

[**DiInstallDriver**](/windows/win32/api/newdev/nf-newdev-diinstalldrivera)

[**SetupDiBuildDriverInfoList**](/windows/win32/api/setupapi/nf-setupapi-setupdibuilddriverinfolist)

[**SetupDiEnumDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinfo)

[**SetupDiEnumDriverInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdriverinfoa)

[**SetupDiGetClassDevs**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsw)

[**SetupDiGetDeviceRegistryProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)

[**SetupDiGetDriverInfoDetail**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdriverinfodetaila)

[**SetupDiOpenDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendeviceinfoa)

[**SetupDiSetSelectedDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdisetselecteddevice)

[**SetupDiSetSelectedDriver**](/windows/win32/api/setupapi/nf-setupapi-setupdisetselecteddrivera)

[**UpdateDriverForPlugAndPlayDevices**](/windows/win32/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)

