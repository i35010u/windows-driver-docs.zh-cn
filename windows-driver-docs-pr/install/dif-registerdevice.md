---
title: DIF_REGISTERDEVICE
description: DIF_REGISTERDEVICE
keywords:
- DIF_REGISTERDEVICE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_REGISTERDEVICE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8294b77f9201e2d008eb4d998f32d472494640c5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834515"
---
# <a name="dif_registerdevice"></a>DIF_REGISTERDEVICE


DIF_REGISTERDEVICE 请求允许安装程序参与使用 PnP 管理器注册新创建的设备实例。 Windows 为非 PnP 设备发送此 DIF 请求。

### <a name="when-sent"></a>发送时间

当安装程序报告以前未知的设备以响应 [**DIF_DETECT**](dif-detect.md) 请求时。 Windows 在 "添加硬件向导" 的 "分析" 阶段发送此 DIF 请求，然后安装设备。 Windows 还会在非 PnP 检测期间发送此请求。

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

<a href="" id="class-installation-parameters-"></a>类安装参数   
无

### <a name="installer-output"></a>安装程序输出

无

### <a name="installer-return-value"></a>安装程序返回值

共同安装程序可以返回 NO_ERROR 或 Win32 错误代码。 对于此 DIF 请求，共同安装程序不应返回 ERROR_DI_POSTPROCESSING_REQUIRED。

如果安装程序确定设备是一个重复设备，则会返回 ERROR_DUPLICATE_FOUND。

如果类安装程序成功处理此请求，并且 [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller) 随后应调用默认处理程序，则类安装程序将返回 ERROR_DI_DO_DEFAULT。

如果类安装程序成功处理此请求（包括直接调用默认处理程序），则类安装程序应返回 NO_ERROR 并且 **SetupDiCallClassInstaller** 将不会再次调用默认处理程序。

**注意**  类安装程序可以直接调用默认处理程序，但类安装程序永远不会尝试取代默认处理程序的操作。

 

有关调用默认处理程序的详细信息，请参阅 [调用默认的 DIF 代码处理程序](./calling-the-default-dif-code-handlers.md)。

如果类安装程序遇到错误，则安装程序应返回相应的 Win32 错误代码，并且 **SetupDiCallClassInstaller** 将不会随后调用默认处理程序。

如果安装程序确定设备是重复的，则安装程序将返回 ERROR_DUPLICATE_FOUND。

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

[**SetupDiRegisterDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)

### <a name="installer-operation"></a>安装程序操作

*设备安装应用程序* 通常发送此 DIF 请求以便向 pnp 管理器注册非 PnP 设备。 从 Microsoft Windows 2000 开始，必须先注册非 PnP 设备，然后才能安装它们。

安装程序通常会处理此 DIF 请求，以进行重复检测。 此类安装程序通常 ([**SetupDiRegisterDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)) 调用默认处理程序，并指定其检测例程。 如果注册成功且安装程序确定设备不是重复设备，安装程序将返回 NO_ERROR。

共同安装程序应执行任何操作以在其预处理过程中处理此 DIF 请求。 当调用共同安装程序进行后处理时，设备实例已由类安装程序或默认处理程序注册。

如果安装程序为此 DIF 代码返回错误，通常 ERROR_DUPLICATE_FOUND，Windows 将从设备信息集中删除该设备。

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


[**DIF_DETECT**](dif-detect.md)

[**SetupDiRegisterDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)

[**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

 

