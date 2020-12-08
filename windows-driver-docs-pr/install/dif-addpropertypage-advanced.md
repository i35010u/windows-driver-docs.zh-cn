---
title: DIF_ADDPROPERTYPAGE_ADVANCED
description: DIF_ADDPROPERTYPAGE_ADVANCED
keywords:
- DIF_ADDPROPERTYPAGE_ADVANCED 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_ADDPROPERTYPAGE_ADVANCED
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 34ccaf97c8f0dab9c5458784c47d286e2ecc44f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827637"
---
# <a name="dif_addpropertypage_advanced"></a>DIF_ADDPROPERTYPAGE_ADVANCED


DIF_ADDPROPERTYPAGE_ADVANCED 请求允许安装程序为设备提供一个或多个自定义属性页。

### <a name="when-sent"></a>发送时间

用户单击设备管理器或控制面板中设备的属性时。

### <a name="who-handles"></a>谁处理

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>类共同安装程序</p></td>
<td align="left"><p>可以处理</p></td>
</tr>
<tr class="even">
<td align="left"><p>设备共同安装程序</p></td>
<td align="left"><p>可以处理</p></td>
</tr>
<tr class="odd">
<td align="left"><p>类安装程序</p></td>
<td align="left"><p>可以处理</p></td>
</tr>
</tbody>
</table>

 

### <a name="installer-input"></a>安装程序输入

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
提供包含设备的 [设备信息集](./device-information-sets.md) 的句柄。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
还可以提供一个指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构在设备信息集中标识设备。 如果 *DeviceInfoSet* 为 **NULL**，则 Windows 将请求 [设备安装程序类](./overview-of-device-setup-classes.md)的属性页。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a))  (设备安装参数与 *DeviceInfoData*（如果已指定）或与 *DeviceInfoSet* 相关联。

<a href="" id="class-installation-parameters"></a>类安装参数  
[**SP_ADDPROPERTYPAGE_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_newdevicewizard_data)结构与 *DeviceInfoData*（如果已指定）或 *DeviceInfoSet* 相关联。

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改设备安装参数。

<a href="" id="class-installation-parameters"></a>类安装参数  
安装程序可以修改 [**SP_ADDPROPERTYPAGE_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_newdevicewizard_data) 以提供自定义页面。

### <a name="installer-return-value"></a>安装程序返回值

共同安装程序可能返回 NO_ERROR 或 Win32 错误。 对于此 DIF 请求，共同安装程序不应返回 ERROR_DI_POSTPROCESSING_REQUIRED。

如果类安装程序成功提供了页面，则它会返回 NO_ERROR。 否则，类安装程序将返回 ERROR_DI_DO_DEFAULT 或 Win32 错误代码。

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

为了响应此 DIF 请求，安装程序可以提供自定义属性页。 通过处理此 DIF 请求，你可以从类安装程序或共同安装程序提供属性页，并不再需要充当属性页提供程序的单独 DLL。

安装程序通常会处理此 DIF 请求，以添加新的特定于设备或特定于安装程序的属性页。 安装程序还可以替换设备的系统提供的 "驱动程序" 属性页、资源属性页或电源属性页。 如果安装程序替换系统提供的页面，则安装程序必须在设备的设备安装参数中设置相应的标志：

<a href="" id="di-driverpage-added"></a>DI_DRIVERPAGE_ADDED  
安装程序提供了驱动程序属性页。

<a href="" id="di-resourcepage-added"></a>DI_RESOURCEPAGE_ADDED  
安装程序提供了资源属性页。

<a href="" id="di-flagsex-powerpage-added"></a>DI_FLAGSEX_POWERPAGE_ADDED  
安装程序提供了电源属性页。

安装程序无法替换系统提供的常规属性页。

Windows 只显示一个驱动程序页、一个资源页和一个设备的一个 power 页。 如果以前的安装程序已提供该类型的页，则安装程序不应提供替换系统页面。 此约束不适用于非系统提供的属性页。

共同安装程序应在其预处理过程中添加自定义页面。

如果安装程序允许用户设置需要 Windows 删除和重新启动设备的属性，则安装程序必须在 **DialogProc** 例程的设备安装参数中设置 DI_FLAGSEX_PROPCHANGE_PENDING 标志。

有关如何提供设备属性页的详细信息，请参阅 [提供设备属性页](./overview-of-device-property-pages.md)。

有关 DIF 代码的详细信息，请参阅 [处理 Dif 代码](./handling-dif-codes.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Microsoft Windows 2000 和更高版本的 Windows 中受支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Setupapi.log (包含 Setupapi.log) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**SP_ADDPROPERTYPAGE_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_newdevicewizard_data)

[**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

