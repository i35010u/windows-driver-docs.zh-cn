---
title: DIF_UNREMOVE
description: DIF_UNREMOVE
ms.assetid: 01e39f77-3ee8-44c4-ba1a-19d4356b26ce
keywords:
- DIF_UNREMOVE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_UNREMOVE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bef1b9d6c5d92bf5e84312a00b9cc1a2ecff3bca
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107172"
---
# <a name="dif_unremove"></a>DIF_UNREMOVE


DIF_UNREMOVE 请求通知安装程序，Windows 将在给定的硬件配置文件中恢复设备，并为安装程序提供参与操作的机会。 Windows 只为非 PnP 设备发送此请求。

### <a name="when-sent"></a>发送时间

根枚举时，非 PnP 设备将恢复为硬件配置文件。

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
[**SP_UNREMOVEDEVICE_PARAMS**](/windows/desktop/api/setupapi/ns-setupapi-_sp_unremovedevice_params)结构与*DeviceInfoData*关联。 必须将 " **作用域** " 字段设置为 "DI_UNREMOVEDEVICE_CONFIGSPECIFIC"，并且必须在 **hwprofile 中** 字段中指定硬件配置文件。

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

[**SetupDiUnremoveDevice**](/windows/desktop/api/setupapi/nf-setupapi-setupdiunremovedevice)

### <a name="installer-operation"></a>安装程序操作

"Unremoving" 设备基本上意味着，Windows 会在特定硬件配置文件中清除先前标记为 "不存在" 的标志。

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


[**SetupDiUnremoveDevice**](/windows/desktop/api/setupapi/nf-setupapi-setupdiunremovedevice)

[**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

[**SP_UNREMOVEDEVICE_PARAMS**](/windows/desktop/api/setupapi/ns-setupapi-_sp_unremovedevice_params)

 

