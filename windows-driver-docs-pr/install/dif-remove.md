---
title: DIF_REMOVE
description: DIF_REMOVE
ms.assetid: 14429756-c059-46d7-bd1c-0ae57d1ec8b5
keywords:
- DIF_REMOVE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_REMOVE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fc772967ee59347bcfc5ce4163b2428e8dbee2e1
ms.sourcegitcommit: 9355a80229bb2384dd45493d36bdc783abdd8d7a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/07/2020
ms.locfileid: "75694239"
---
# <a name="dif_remove"></a>DIF_REMOVE


DIF_REMOVE 请求通知安装程序 Windows 即将删除设备，并为该安装程序提供了为删除做准备的机会。

### <a name="when-sent"></a>发送时间

当用户设备管理器中删除设备时。

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
为包含要删除的设备的[设备信息集](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)提供一个句柄。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
在设备信息集中提供设备的[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)结构的指针。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
与*DeviceInfoData*关联的设备安装参数（[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)）。

<a href="" id="class-installation-parameters"></a>类安装参数  
[**SP_REMOVEDEVICE_PARAMS**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_removedevice_params)结构可能与*DeviceInfoData*关联。

如果[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)中 DI_CLASSINSTALLPARAMS 标志清晰，则不存在请求的类安装参数。 在这种情况下，未指定硬件配置文件，并且设备将作为一个整体从系统中删除。

### <a name="installer-output"></a>安装程序输出

<a href="" id="none"></a>内容  

### <a name="installer-return-value"></a>安装程序返回值

共同安装程序可以返回 NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

如果类安装程序成功处理此请求，并且[**SetupDiCallClassInstaller**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)随后应调用默认处理程序，则类安装程序将返回 ERROR_DI_DO_DEFAULT。

如果类安装程序成功处理此请求（包括直接调用默认处理程序），则类安装程序应返回 NO_ERROR 并且**SetupDiCallClassInstaller**将不会再次调用默认处理程序。

**请注意**   类安装程序可以直接调用默认处理程序，但类安装程序永远不会尝试取代默认处理程序的操作。

 

有关调用默认处理程序的详细信息，请参阅[调用默认的 DIF 代码处理程序](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)。

如果类安装程序遇到错误，则安装程序应返回相应的 Win32 错误代码，并且**SetupDiCallClassInstaller**将不会随后调用默认处理程序。

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

[**SetupDiRemoveDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice)

### <a name="installer-operation"></a>安装程序操作

为了响应 DIF_REMOVE 请求，安装程序通常会执行一些清理操作。 在这种情况下，共同安装程序返回 NO_ERROR 并且类安装程序返回 ERROR_DI_DO_DEFAULT。

如果安装程序确定不应删除该设备，则安装程序将通过返回 Win32 错误代码来使该方法失败。 如果 DI_QUIETINSTALL 标志清晰，则安装程序应向用户显示一条消息，说明未删除设备的原因。

共同安装程序不得尝试通过调用**SetupDiRemoveDevice**来删除设备本身。 在成功删除设备后，共同安装程序通常会在后处理时处理此请求。

例如，如果共同安装程序必须删除注册表中的信息，则共同安装程序应在执行后处理时执行此操作，并且仅当前面的安装程序成功删除请求时才这样做。 在预处理过程中，共同安装程序应将注册表信息存储在其上下文参数中，并返回 ERROR_DI_POSTPROCESSING_REQUIRED 以请求后处理。 当 Windows 调用共同安装程序来后处理此 DIF 请求时，共同安装程序应检查是否 NO_ERROR 了 DIF 状态，然后再删除注册表信息。 如果共同安装程序在其预处理过程中删除注册表信息，并且类安装程序（或其他共同安装程序）未通过 DIF_REMOVE，则共同安装程序可能会使设备处于不可预知的状态。

如果文件被另一台设备使用，则在处理此 DIF 请求时，安装程序不应删除文件。

Windows 在启动 PnP 查询-删除和删除处理之前会发送此 DIF 请求。

有关 DIF 代码的详细信息，请参阅[处理 Dif 代码](https://docs.microsoft.com/windows-hardware/drivers/install/handling-dif-codes)。

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
<td align="left"><p>Header</p></td>
<td align="left">Setupapi.log （包括 Setupapi.log）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**SetupDiRemoveDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

[**SP_REMOVEDEVICE_PARAMS**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_removedevice_params)

 

 






