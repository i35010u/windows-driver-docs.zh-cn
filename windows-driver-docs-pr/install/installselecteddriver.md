---
title: InstallSelectedDriver 函数
description: InstallSelectedDriver 函数将所选的设备上安装所选驱动程序。
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
ms.openlocfilehash: e47d1c83babe694ba9e3a99fe0dd5aa11c026338
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525218"
---
# <a name="installselecteddriver-function"></a>InstallSelectedDriver 函数


**InstallSelectedDriver**函数已弃用。 适用于 Windows Vista 和更高版本，使用[ **DiInstallDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff544710)相反。

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

*hwndParent* \[in\]  
顶级窗口的句柄的**InstallSelectedDriver**函数用于显示与安装驱动程序相关联的用户界面组件。

*DeviceInfoSet* \[in\]  
句柄[设备信息集](https://msdn.microsoft.com/library/windows/hardware/ff541247)，其中包含表示所选的设备和设备的所选驱动程序的设备信息元素。 有关如何选择设备和设备的驱动程序的详细信息，请参阅以下**备注**部分。

*保留*\[中\]  
此参数必须设置为**NULL**。

*备份*\[中\]  
类型为布尔值，用于确定的值是否**InstallSelectedDriver**函数安装在设备的所选驱动程序之前备份所选设备的当前安装的驱动程序。 如果当前安装的驱动程序来备份和用户遇到问题时使用新的驱动程序，用户可以回滚新的驱动程序的安装到备份驱动程序。 如果不会备份当前安装的驱动程序，用户不能回滚新的驱动程序安装到以前安装的驱动程序。 如果*备份*设置为**TRUE**， **InstallSelectedDriver**备份当前安装的驱动程序; 否则，该函数不会备份当前已安装驱动程序。 有关驱动程序的详细信息的备份，请参阅**DiRollbackDriver**。

*bReboot* \[out\]  
对变量的类型为 DWORD 的指针， **InstallSelectedDriver**集以指示是否需要重新启动系统才能完成安装。 如果将变量设置为 DI\_NEEDREBOOT，系统重新启动是必需的; 否则，不需要重新启动系统。 调用方负责在系统重新启动。

<a name="return-value"></a>返回值
------------

**InstallSelectedDriver**将返回**TRUE**如果所选驱动程序已安装在所选的设备; 否则，该函数返回**FALSE** ，并且可以通过使检索所记录的错误调用**GetLastError**。

一些较常见的错误值的**GetLastError**可能会返回如下所示：

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
<td align="left"><p>所选驱动程序是更好地与匹配的驱动程序比以前已安装在设备的驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ERROR_IN_WOW64</strong></td>
<td align="left"><p>调用应用程序是尝试在 64 位环境中，这不允许执行一个 32 位应用程序。 有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff541255" data-raw-source="[Installing Devices on 64-Bit Systems](https://msdn.microsoft.com/library/windows/hardware/ff541255)">64 位系统上安装设备</a>。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

访问**InstallSelectedDriver**，调用**LoadLibrary**加载*Newdev.dll* ，然后调用**GetProcAddress**获取函数指向**InstallSelectedDriver**。

只应调用**InstallSelectedDriver**是否需要特定的设备上安装特定驱动程序。

**重要**   For Windows Vista 和更高版本的 Windows，则调用[ **DiInstallDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff544710)而不是**InstallSelectedDriver**到执行此类型的操作。

 

以外的特殊应用程序需要特定的设备上的特定驱动程序安装，安装应用程序应安装最匹配的设备驱动程序。 若要安装的驱动程序是设备的最佳匹配项，请调用[ **DiInstallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff544717)或[ **UpdateDriverForPlugAndPlayDevices**](https://msdn.microsoft.com/library/windows/hardware/ff553534)。 有关哪些这些函数来调用设备上安装驱动程序的详细信息，请参阅[安装程序 Api 函数的简化驱动程序安装](https://msdn.microsoft.com/library/windows/hardware/ff550867)。

然后再调用**InstallSelectedDriver**，调用方必须获取包含该设备的设备信息集，在组中，选择设备，并选择设备的驱动程序。

若要创建包含设备的设备信息集，请执行以下操作：

-   调用[ **SetupDiGetClassDevs** ](https://msdn.microsoft.com/library/windows/hardware/ff551069)若要检索包含设备的设备信息集，然后调用[ **SetupDiEnumDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff551010)枚举中的设备信息集的设备。 在每次调用**SetupDiEnumDeviceInfo**返回 SP\_DEVINFO\_数据结构，它表示枚举的设备中设备的信息集。 若要获取有关枚举设备的特定信息，请调用[ **SetupDiGetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551967) ，并提供 SP\_DEVINFO\_返回的数据结构通过**SetupDiEnumDeviceInfo**。

    - 或 -

-   调用[ **SetupDiOpenDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff552071)将具有已知的设备实例 ID 的设备添加到设备的信息集。 **SetupDiOpenDeviceInfo**将返回[ **SP\_DEVINFO\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff552344)结构，它表示设备信息设置中的设备。

获取 SP 后\_DEVINFO\_对于设备，请调用的数据结构[ **SetupDiSetSelectedDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff552176)设备信息集中选择的设备。

若要检索设备的驱动程序，请调用[ **SetupDiBuildDriverInfoList** ](https://msdn.microsoft.com/library/windows/hardware/ff550917)若要生成的设备兼容的驱动程序的列表，然后调用[ **SetupDiEnumDriverInfo**](https://msdn.microsoft.com/library/windows/hardware/ff551018)枚举设备驱动程序列表中的元素。 对于每个枚举驱动程序， **SetupDiEnumDriverInfo**检索 SP\_DRVINFO\_数据结构，它表示该驱动程序。 [**SetupDiGetDriverInfoDetail** ](https://msdn.microsoft.com/library/windows/hardware/ff551973)可以调用以检索有关枚举驱动程序的其他详细信息。

获取 SP 后\_DRVINFO\_驱动程序调用的数据结构[ **SetupDiSetSelectedDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff552183)以选择设备的驱动程序。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Microsoft Windows 2000 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">无 ( <strong>InstallSelectedDriver</strong>函数未在公共标头文件中定义。 有关详细信息，请参阅<strong>备注</strong>部分。 )</td>
</tr>
<tr class="even">
<td align="left"><p>Library</p></td>
<td align="left">Newdev.lib</td>
</tr>
<tr class="odd">
<td align="left"><p>DLL</p></td>
<td align="left">Newdev.dll</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**DiInstallDevice**](https://msdn.microsoft.com/library/windows/hardware/ff544710)

[**DiInstallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff544717)

[**SetupDiBuildDriverInfoList**](https://msdn.microsoft.com/library/windows/hardware/ff550917)

[**SetupDiEnumDeviceInfo**](https://msdn.microsoft.com/library/windows/hardware/ff551010)

[**SetupDiEnumDriverInfo**](https://msdn.microsoft.com/library/windows/hardware/ff551018)

[**SetupDiGetClassDevs**](https://msdn.microsoft.com/library/windows/hardware/ff551069)

[**SetupDiGetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551967)

[**SetupDiGetDriverInfoDetail**](https://msdn.microsoft.com/library/windows/hardware/ff551973)

[**SetupDiOpenDeviceInfo**](https://msdn.microsoft.com/library/windows/hardware/ff552071)

[**SetupDiSetSelectedDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552176)

[**SetupDiSetSelectedDriver**](https://msdn.microsoft.com/library/windows/hardware/ff552183)

[**UpdateDriverForPlugAndPlayDevices**](https://msdn.microsoft.com/library/windows/hardware/ff553534)

 

 






