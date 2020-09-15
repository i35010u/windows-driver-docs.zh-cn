---
title: DIF_INSTALLDEVICEFILES
description: DIF_INSTALLDEVICEFILES
ms.assetid: 544a9a88-156e-494d-9ef0-8070addfa86b
keywords:
- DIF_INSTALLDEVICEFILES 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_INSTALLDEVICEFILES
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 73075a6279c97927591bd0ad57df7fafaf67369d
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107294"
---
# <a name="dif_installdevicefiles"></a>DIF_INSTALLDEVICEFILES


DIF_INSTALLDEVICEFILES 请求允许安装程序参与复制文件以支持设备，或创建设备的文件列表。 设备文件包括所选驱动程序的文件、任何设备接口和所有共同安装程序。

### <a name="when-sent"></a>发送时间

[系统提供的设备安装组件](./system-provided-device-installation-components.md)发送此 DIF 请求的原因有多种。 某些设备安装组件会在 DIF_REGISTER_COINSTALLERS、DIF_INSTALLINTERFACES 和 DIF_INSTALL_DEVICE 之前发送此 DIF 请求，以确保在继续安装之前可以复制所有相关文件。 某些设备安装组件省略此 DIF 请求，并期望在处理这三个 DIF 请求的过程中复制文件。 此外，某些设备安装组件会发送此 DIF 请求，以检索与设备相关联的文件的列表。

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
提供 [设备信息集](./device-information-sets.md) 的句柄，其中包含要复制其支持文件的设备。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
提供一个指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构在设备信息集中标识设备。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
与*DeviceInfoData*关联的设备安装参数 ([**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)) 。

如果设置了 DI_NOVCP 标志，则设备安装参数包含有效的 **FileQueue** 句柄，处理此 DIF 请求的安装程序会将其文件操作添加到此队列中，并且不提交队列。

<a href="" id="class-installation-parameters"></a>类安装参数  
无

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters-"></a>设备安装参数   
安装程序可以修改 **FileQueue**（如果有）。

### <a name="installer-return-value"></a>安装程序返回值

共同安装程序可以返回 NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

如果类安装程序成功处理此请求，并且 [**SetupDiCallClassInstaller**](/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller) 随后应调用默认处理程序，则类安装程序将返回 ERROR_DI_DO_DEFAULT。

如果类安装程序成功处理此请求（包括直接调用默认处理程序），则类安装程序应返回 NO_ERROR 并且 **SetupDiCallClassInstaller** 将不会再次调用默认处理程序。

**注意**   类安装程序可以直接调用默认处理程序，但类安装程序永远不会尝试取代默认处理程序的操作。

 

有关调用默认处理程序的详细信息，请参阅 [调用默认的 DIF 代码处理程序](./calling-the-default-dif-code-handlers.md)。

如果类安装程序遇到错误，则安装程序应返回相应的 Win32 错误代码，并且 **SetupDiCallClassInstaller** 将不会随后调用默认处理程序。

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

[**SetupDiInstallDriverFiles**](/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldriverfiles)

### <a name="installer-operation"></a>安装程序操作

为响应 DIF_INSTALLDEVICEFILES 请求，安装程序指定任何必要的文件操作。 例如，安装程序可以指定要复制的、设备安装所需的其他文件。 如果设置了 DI_NOVCP 标志，则安装程序会通过将其添加到设备安装参数中的 **FileQueue** 来指定文件操作。 请参阅 Microsoft Windows SDK，了解有关如何使用文件队列和文件队列功能（如 **SetupInstallFilesFromInfSection**）的参考页的信息。

如果在设备安装过程中发送此 DIF 请求，并且安装程序返回 Microsoft Win32 错误代码，则 Windows 将停止安装。

如果 [系统提供的设备安装组件](./system-provided-device-installation-components.md) 发送此 DIF 请求来检索与设备关联的文件列表，则该组件将检索文件队列，但不会提交队列。

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


[**SetupDiInstallDriverFiles**](/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldriverfiles)

[**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

 

