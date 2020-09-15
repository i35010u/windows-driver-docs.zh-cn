---
title: DIF_ALLOW_INSTALL
description: DIF_ALLOW_INSTALL
ms.assetid: 0bcda90e-f9f1-4965-a08b-d884077a2e8b
keywords:
- DIF_ALLOW_INSTALL 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_ALLOW_INSTALL
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 112f8374cc5d8d9822311abb0bfd70d420efaa86
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106962"
---
# <a name="dif_allow_install"></a>DIF_ALLOW_INSTALL


DIF_ALLOW_INSTALL 请求要求设备安装程序是否可以继续安装设备。

### <a name="when-sent"></a>发送时间

选择设备驱动程序之后，在安装设备之前。

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
<td align="left"><p>不应处理</p></td>
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
无

### <a name="installer-output"></a>安装程序输出

<a href="" id="none"></a>内容  

### <a name="installer-return-value"></a>安装程序返回值

共同安装程序可能返回 NO_ERROR 或 Win32 错误。 对于此 DIF 请求，共同安装程序不应返回 ERROR_DI_POSTPROCESSING_REQUIRED。

类安装程序通常返回 ERROR_DI_DO_DEFAULT 或 Win32 错误代码。

此 DIF 请求的典型 Win32 错误代码包括 ERROR_DI_DONT_INSTALL 和 ERROR_NON_WINDOWS_NT_DRIVER。

**注意**   类安装程序和共同安装程序不应 freturn ERROR_REQUIRES_INTERACTIVE_WINDOWSTATION 因为这会导致设备安装失败。 如果设备安装需要用户交互，则类安装程序和共同安装程序应支持 " [完成-安装" 操作](./finish-install-actions--windows-vista-and-later-.md)。

 

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

为响应 DIF_ALLOW_INSTALL 请求，安装程序将确认 Windows 是否可以安装该设备。

如果安装程序确定所选的驱动程序不正确 (例如，如果该驱动程序是仅限 Windows 9x 的驱动程序，将无法在基于 NT 的操作系统上正常运行，则安装程序可能会失败此请求) 或确定所选的驱动程序是否存在 bug。

如果在设备安装参数中设置了 DI_QUIETINSTALL 标志，并且安装程序必须在设备安装过程中显示 UI，则安装程序可能会导致此请求失败。 但是，这种故障很少见，因为安装程序通常可以提供任何 UI 页来响应 DIF_NEWDEVICEWIZARD_FINISHINSTALL 请求。 在这种情况下，UI 不会阻止安装程序成功执行为其设置了 quiet 标志的 DIF_ALLOW_INSTALL 请求。 但是，如果安装程序无法将其 UI 限制为完成安装用例，则在设置了 DI_QUIETINSTALL 标志的情况下，安装程序必须失败此 DIF 请求。 例如，如果某个安装程序调用了由供应商提供的显示 UI 的代码，则可能会有此限制。

如果安装程序未能通过此 DIF 请求，则 Windows 将停止安装。

如果安装程序未能通过此 DIF 请求并 DI_QUIETINSTALL 未在设备安装参数中设置，则安装程序应显示一个对话框，其中包含一条说明设备未安装的原因的消息。

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


[**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

 

