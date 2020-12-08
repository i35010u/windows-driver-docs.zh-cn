---
title: DIF_NEWDEVICEWIZARD_SELECT
description: DIF_NEWDEVICEWIZARD_SELECT
keywords:
- DIF_NEWDEVICEWIZARD_SELECT 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_NEWDEVICEWIZARD_SELECT
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8e63051e7e1382cc69e41d9f48e42db50f214a70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782785"
---
# <a name="dif_newdevicewizard_select"></a>DIF_NEWDEVICEWIZARD_SELECT


DIF_NEWDEVICEWIZARD_SELECT 请求允许安装程序提供 (s) 替换标准选择驱动程序页的自定义向导页。 此请求仅在手动安装非 PnP 设备期间使用。

### <a name="when-sent"></a>发送时间

紧靠 Windows 之前，会显示 "选择设备驱动程序" 页。

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
<td align="left"><p>不处理</p></td>
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
提供一个指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构在设备信息集中标识设备。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
与 *DeviceInfoData* 关联的设备安装参数 ([**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)) 。

<a href="" id="class-installation-parameters"></a>类安装参数  
[**SP_NEWDEVICEWIZARD_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_newdevicewizard_data)结构与 *DeviceInfoData* 关联。

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改设备安装参数中的标志。 Windows 在完成此 DIF 请求后不检查标志。 不过，稍后会在安装过程中检查它们。

<a href="" id="class-installation-parameters"></a>类安装参数  
安装程序可以修改 [**SP_NEWDEVICEWIZARD_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_newdevicewizard_data) 以提供) 的自定义页 (。

### <a name="installer-return-value"></a>安装程序返回值

如果联合安装程序不处理此 DIF 请求，则会从其预处理传递 NO_ERROR。 如果共同安装程序处理此请求，它可以返回 NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

如果类安装程序成功提供了 () 的页，则它会返回 NO_ERROR。 否则，类安装程序将返回 ERROR_DI_DO_DEFAULT 或 Win32 错误代码。

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

DIF_NEWDEVICEWIZARD_SELECT 请求允许安装程序提供 (s) 替换标准选择驱动程序页的自定义向导页。 此请求仅在手动安装非 PnP 设备期间使用。

安装程序将响应此 DIF 请求，以完全替换标准的 "选择驱动程序向导" 页。 相反，安装程序只需修改标准页或修改要从中进行选择的驱动程序的列表，安装程序就应该在响应 [**DIF_SELECTDEVICE**](dif-selectdevice.md) 请求时执行此操作。

共同安装程序应在其后处理过程中添加自定义页面 () ，且仅当类安装程序未将自定义 (页面添加到) 时才添加。 如果类安装程序添加了)  (的页，则共同安装程序不应这样做。 否则，系统可能会要求用户选择一个驱动程序两次。

如果安装程序提供自定义的 "选择" 页，则安装程序必须设置所选的驱动程序。 在安装程序支持该向导页的代码中，在用户单击 " **下一步**" 后，安装程序必须调用 [**SetupDiSetSelectedDriver**](/windows/win32/api/setupapi/nf-setupapi-setupdisetselecteddrivera)。

安装程序应在自定义向导页的 PROPSHEETPAGE 结构中提供向导97标题标题和标题副标题。 安装程序不应替换系统提供的向导标题。 请参阅 PROPSHEETPAGE 结构的相关文档的 Microsoft Windows SDK，并了解有关属性页的详细信息。

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


[**DIF_NEWDEVICEWIZARD_PREANALYZE**](dif-newdevicewizard-preanalyze.md)

[**DIF_NEWDEVICEWIZARD_PRESELECT**](dif-newdevicewizard-preselect.md)

[**DIF_NEWDEVICEWIZARD_POSTANALYZE**](dif-newdevicewizard-postanalyze.md)

[**DIF_SELECTDEVICE**](dif-selectdevice.md)

[**SetupDiSetSelectedDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdisetselecteddevice)

[**SetupDiSetSelectedDriver**](/windows/win32/api/setupapi/nf-setupapi-setupdisetselecteddrivera)

[**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

[**SP_NEWDEVICEWIZARD_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_newdevicewizard_data)

 

