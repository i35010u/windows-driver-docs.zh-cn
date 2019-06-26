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
ms.openlocfilehash: 1f8841725e55efe62b2c6317be5c62cbecea1c32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387052"
---
# <a name="difinstalldevicefiles"></a>DIF_INSTALLDEVICEFILES


DIF_INSTALLDEVICEFILES 请求可让安装程序来参与复制文件以支持设备或设备的文件的列表。 设备文件包括为所选驱动程序、 任何设备接口和任何共同安装程序。

### <a name="when-sent"></a>发送时间

[系统提供的设备安装组件](https://docs.microsoft.com/windows-hardware/drivers/install/system-provided-device-installation-components)发送的原因有多种此 DIF 请求。 某些设备安装组件之前 DIF_REGISTER_COINSTALLERS、 DIF_INSTALLINTERFACES 和 DIF_INSTALL_DEVICE，以确保所有相关文件，可以复制在继续安装之前发送此 DIF 请求。 设备安装的一些组件忽略此 DIF 请求，并期望在三个对这些差异请求处理期间复制的文件。 此外，某些设备安装组件发送此 DIF 请求以检索与设备关联的文件的列表。

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
提供的句柄[设备信息集](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)，其中包含其支持的文件是要复制的设备。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
提供一个指向[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)标识设备中设备的信息集的结构。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) 与关联*DeviceInfoData*。

如果设置了 DI_NOVCP 标志，设备安装参数包含有效**FileQueue**句柄和处理此 DIF 请求的安装程序将其文件操作添加到此队列并不提交队列。

<a href="" id="class-installation-parameters"></a>类的安装参数  
无

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters-"></a>设备安装参数   
安装程序可以修改**FileQueue**，如果存在。

### <a name="installer-return-value"></a>安装程序返回值

辅助安装程序可以返回 NO_ERROR、 ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

如果类安装程序已成功处理此请求并[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)应随后调用默认处理程序类安装程序将返回 ERROR_DI_DO_DEFAULT。

类安装程序类安装程序将成功处理此请求，包括直接调用默认处理程序，如果应返回 NO_ERROR 并**SetupDiCallClassInstaller**随后不会调用默认处理程序电子邮件了。

**请注意**  类安装程序可以直接调用默认处理程序，但类安装程序应永远不会尝试取代默认处理程序的操作。

 

调用默认处理程序的详细信息，请参阅[调用默认 DIF 代码处理程序](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)。

安装程序类安装程序遇到错误，如果应返回相应的 Win32 错误代码和**SetupDiCallClassInstaller**随后不会调用默认处理程序。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

[**SetupDiInstallDriverFiles**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldriverfiles)

### <a name="installer-operation"></a>安装程序操作

在响应中到 DIF_INSTALLDEVICEFILES 请求安装程序指定任何必需的文件操作。 例如，安装程序可以指定所需的设备安装的要复制的其他文件。 如果设置了 DI_NOVCP 标志，安装程序通过将它们添加到指定文件操作**FileQueue**中设备安装参数。 请参阅 Microsoft Windows SDK 有关如何使用文件队列的信息和参考页文件队列功能在如**SetupInstallFilesFromInfSection**。

如果在设备安装过程中发送此 DIF 请求和安装程序将返回 Microsoft Win32 错误代码，Windows 将停止安装。

如果[系统提供的设备安装组件](https://docs.microsoft.com/windows-hardware/drivers/install/system-provided-device-installation-components)发送此 DIF 请求来检索与设备相关联的文件的列表，该组件检索文件队列，但不会提交队列。

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


[**SetupDiInstallDriverFiles**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldriverfiles)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






