---
title: DIF_POWERMESSAGEWAKE
description: DIF_POWERMESSAGEWAKE
ms.assetid: 73f6e763-0900-4297-ac88-20bbb3ac424d
keywords:
- DIF_POWERMESSAGEWAKE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_POWERMESSAGEWAKE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2c9f780dced67e5c2f6cd92f1c284860e52cb586
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107504"
---
# <a name="dif_powermessagewake"></a>DIF_POWERMESSAGEWAKE


DIF_POWERMESSAGEWAKE 请求允许安装程序提供 Windows 在设备属性的 "电源管理" 属性页上显示的自定义文本。

### <a name="when-sent"></a>发送时间

当用户单击菜单项或选项卡以显示设备的属性时。

如果设备的驱动程序支持电源管理，Windows 只会发送此 DIF 请求。 否则，Windows 不会显示设备的任何电源属性。

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
提供一个指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构在设备信息集中标识设备。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
与*DeviceInfoData*关联的设备安装参数 ([**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)) 。

<a href="" id="class-installation-parameters"></a>类安装参数  
[**SP_POWERMESSAGEWAKE_PARAMS**](/windows/desktop/api/setupapi/ns-setupapi-_sp_powermessagewake_params_a)结构与*DeviceInfoData*关联。

### <a name="installer-output"></a>安装程序输出

<a href="" id="class-installation-parameters"></a>类安装参数  
安装程序可以修改 [**SP_POWERMESSAGEWAKE_PARAMS**](/windows/desktop/api/setupapi/ns-setupapi-_sp_powermessagewake_params_a) 以提供设备的电源属性页的自定义文本。

### <a name="installer-return-value"></a>安装程序返回值

共同安装程序通常返回 NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

如果类安装程序成功提供了 power properties 文本，则它会返回 NO_ERROR。 否则，类安装程序将返回 ERROR_DI_DO_DEFAULT 或 Win32 错误代码。

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

DIF_POWERMESSAGEWAKE 请求允许安装程序提供 Windows 在设备的电源属性页面上显示的文本。

如果共同安装程序提供了电源属性文本，它应在其后处理阶段执行此操作。 在将处理请求的安装程序提供的任何电源属性文本覆盖到共同安装程序之前，共同安装程序应小心。

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

## <a name="see-also"></a>另请参阅


[**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

[**SP_POWERMESSAGEWAKE_PARAMS**](/windows/desktop/api/setupapi/ns-setupapi-_sp_powermessagewake_params_a)

 

