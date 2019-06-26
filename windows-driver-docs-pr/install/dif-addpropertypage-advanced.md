---
title: DIF_ADDPROPERTYPAGE_ADVANCED
description: DIF_ADDPROPERTYPAGE_ADVANCED
ms.assetid: d2b05c45-3536-4997-ac6f-a5b5c95a97da
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
ms.openlocfilehash: 4dfc26c47c1983b728f78af6103142fa40e1f8c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372729"
---
# <a name="difaddpropertypageadvanced"></a>DIF_ADDPROPERTYPAGE_ADVANCED


DIF_ADDPROPERTYPAGE_ADVANCED 请求可让安装程序提供一个或多个设备的自定义属性页。

### <a name="when-sent"></a>发送时间

当用户单击设备管理器中或在控制面板中的设备的属性。

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
提供的句柄[设备信息集](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)，其中包含该设备。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
根据需要提供一个指向[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)标识设备中设备的信息集的结构。 如果*DeviceInfoSet*是**NULL**，Windows 正在请求的属性页[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) 与关联*DeviceInfoData*、 如果指定，或与*DeviceInfoSet*.

<a href="" id="class-installation-parameters"></a>类的安装参数  
[ **SP_ADDPROPERTYPAGE_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_newdevicewizard_data)与关联结构*DeviceInfoData*、 如果指定，或与*DeviceInfoSet*。

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改设备的安装参数。

<a href="" id="class-installation-parameters"></a>类的安装参数  
安装程序可以修改[ **SP_ADDPROPERTYPAGE_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_newdevicewizard_data)提供自定义页。

### <a name="installer-return-value"></a>安装程序返回值

辅助安装程序可以返回 NO_ERROR 或 Win32 错误。 辅助安装程序不应返回 ERROR_DI_POSTPROCESSING_REQUIRED 此 DIF 请求。

类安装程序返回 NO_ERROR，如果它已成功提供页面。 否则，类安装程序将返回 ERROR_DI_DO_DEFAULT 或 Win32 错误代码。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

在此差异请求响应安装程序可以提供自定义属性页。 处理此 DIF 请求可用于提供从类安装程序或辅助安装程序的属性页，并且无需单独的 DLL 充当属性页提供程序。

安装程序通常会处理此差异的请求添加新的特定于设备的或特定于安装程序的类的属性页。 安装程序还可以替换系统提供的驱动程序属性页、 资源属性页上或设备的 power 属性页。 如果安装程序代替系统提供的页上，安装程序必须设置适当的标志的设备中设备的安装参数：

<a href="" id="di-driverpage-added"></a>DI_DRIVERPAGE_ADDED  
安装程序提供驱动程序属性页。

<a href="" id="di-resourcepage-added"></a>DI_RESOURCEPAGE_ADDED  
安装程序提供资源属性页。

<a href="" id="di-flagsex-powerpage-added"></a>DI_FLAGSEX_POWERPAGE_ADDED  
安装程序提供电源属性页。

安装程序无法替换系统提供的常规属性页。

Windows 仅显示一个驱动程序页、 一个资源页上和设备的一个 power 页。 如果以前的安装程序已提供该类型的页面，安装程序不应提供替换系统页面。 此约束不适用于非系统提供的属性页。

辅助安装程序应在其预处理阶段中添加自定义页。

如果安装程序允许用户将需要删除并重新启动设备的 Windows 属性设置，安装程序必须设置 DI_FLAGSEX_PROPCHANGE_PENDING 标志的设备中安装参数从其**DialogProc**例程.

有关如何提供设备属性页的详细信息，请参阅[提供的设备属性页](https://docs.microsoft.com/windows-hardware/drivers/install/providing-device-property-pages)。

有关差异代码的详细信息，请参阅[处理 DIF 代码](https://docs.microsoft.com/windows-hardware/drivers/install/handling-dif-codes)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>Microsoft Windows 2000 和更高版本的 Windows 支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Setupapi.h （包括 Setupapi.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**SP_ADDPROPERTYPAGE_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_newdevicewizard_data)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






