---
title: DIF_PROPERTYCHANGE
description: DIF_PROPERTYCHANGE
ms.assetid: 62f3380d-8cd1-4f4c-a727-1285de081b9e
keywords:
- DIF_PROPERTYCHANGE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_PROPERTYCHANGE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ddfa8bc7bb9beef04ab75ccddddf9a3172a23ea2
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104786"
---
# <a name="dif_propertychange"></a>DIF_PROPERTYCHANGE


DIF_PROPERTYCHANGE 请求通知安装程序设备的属性正在更改。 设备正在启用、已禁用、已启动、已停止，或属性页上的某些项已更改。 此 DIF 请求使安装程序有机会参与更改。

### <a name="when-sent"></a>发送时间

设备启用、禁用、重新启动、停止或其属性已更改时。

例如，当属性页提供程序在设备的[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)结构的**FLAGSEX**字段中设置 DI_FLAGSEX_PROPCHANGE_PENDING 标志时，Windows 将发送此请求。

有关在第一次启动或重新启动设备时检测到设备的详细信息，请参阅安装程序操作部分。

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
在设备信息集中提供设备的 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
与*DeviceInfoData*关联的设备安装参数 ([**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)) 。

<a href="" id="class-installation-parameters"></a>类安装参数  
[**SP_PROPCHANGE_PARAMS**](/windows/desktop/api/setupapi/ns-setupapi-_sp_propchange_params)结构与*DeviceInfoData*关联。

### <a name="installer-output"></a>安装程序输出

<a href="" id="none"></a>内容  

### <a name="installer-return-value"></a>安装程序返回值

共同安装程序可以返回 NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

如果类安装程序成功处理此请求，并且 [**SetupDiCallClassInstaller**](/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller) 随后应调用默认处理程序，则类安装程序将返回 ERROR_DI_DO_DEFAULT。

如果类安装程序成功处理此请求（包括直接调用默认处理程序），则类安装程序应返回 NO_ERROR 并且 **SetupDiCallClassInstaller** 将不会再次调用默认处理程序。

**注意**   类安装程序可以直接调用默认处理程序，但类安装程序永远不会尝试取代默认处理程序的操作。

 

有关调用默认处理程序的详细信息，请参阅 [调用默认的 DIF 代码处理程序](./calling-the-default-dif-code-handlers.md)。

如果类安装程序遇到错误，则安装程序应返回相应的 Win32 错误代码，并且 **SetupDiCallClassInstaller** 将不会随后调用默认处理程序。

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

[**SetupDiChangeState**](/windows/desktop/api/setupapi/nf-setupapi-setupdichangestate)

### <a name="installer-operation"></a>安装程序操作

为了响应 DIF_PROPERTYCHANGE 请求，安装程序可以参与属性更改操作。 类安装参数 (SP_PROPCHANGE_PARAMS) 指示发生了哪些更改。

属性更改可能需要重新启动系统。 有关如何重新启动系统的信息，请参阅 [**SetupDiCallClassInstaller**](/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)。

当 Windows 首次发送 DIF_INSTALLDEVICE 请求来安装设备时，Windows 将启动该设备，但不会在安装过程中发送 DIF_PROPERTYCHANGE 请求。 如果在设备首次启动时必须执行自定义安装操作，并在每次重新启动设备时，安装程序或共同安装程序应处理第一次启动设备的 DIF_INSTALLDEVICE 请求，并提供一个 DIF_PROPERTYCHANGE 请求，指示状态更改操作是设备正在启动。

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


[**SetupDiChangeState**](/windows/desktop/api/setupapi/nf-setupapi-setupdichangestate)

[**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

[**SP_PROPCHANGE_PARAMS**](/windows/desktop/api/setupapi/ns-setupapi-_sp_propchange_params)

 

