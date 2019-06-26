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
ms.openlocfilehash: ae9b8b778e45d8343faeafc1811f769322ae1ed0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387037"
---
# <a name="difremove"></a>DIF_REMOVE


DIF_REMOVE 请求通知安装程序，Windows 将要删除设备，并使安装程序有机会删除准备。

### <a name="when-sent"></a>发送时间

当用户删除设备在设备管理器。

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
提供的句柄[设备信息集](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)，其中包含要删除的设备。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
提供一个指向[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)设备中设备的信息集的结构。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) 与关联*DeviceInfoData*。

<a href="" id="class-installation-parameters"></a>类的安装参数  
[ **SP_REMOVEDEVICE_PARAMS** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_removedevice_params)结构可能与关联*DeviceInfoData*。

不没有请求任何类安装参数如果 DI_CLASSINSTALLPARAMS 标志明确[ **SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)。 在这种情况下，指定硬件配置文件，并且设备将从整个系统中删除。

### <a name="installer-output"></a>安装程序输出

<a href="" id="none"></a>无  

### <a name="installer-return-value"></a>安装程序返回值

辅助安装程序可以返回 NO_ERROR、 ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

如果类安装程序已成功处理此请求并[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)应随后调用默认处理程序类安装程序将返回 ERROR_DI_DO_DEFAULT。

类安装程序类安装程序将成功处理此请求，包括直接调用默认处理程序，如果应返回 NO_ERROR 并**SetupDiCallClassInstaller**随后不会调用默认处理程序电子邮件了。

**请注意**  类安装程序可以直接调用默认处理程序，但类安装程序应永远不会尝试取代默认处理程序的操作。

 

调用默认处理程序的详细信息，请参阅[调用默认 DIF 代码处理程序](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)。

安装程序类安装程序遇到错误，如果应返回相应的 Win32 错误代码和**SetupDiCallClassInstaller**随后不会调用默认处理程序。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

[**SetupDiRemoveDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice)

### <a name="installer-operation"></a>安装程序操作

在对 DIF_REMOVE 请求的响应，安装程序通常执行某些清除操作。 在这种情况下，辅助安装程序返回 NO_ERROR 和类安装程序将返回 ERROR_DI_DO_DEFAULT。

如果安装程序确定不应删除该设备，安装程序失败并 DIF 请求返回 Win32 错误代码。 如果清除 DI_QUIETINSTALL 标志，则安装程序应显示一条消息，向用户解释了为什么不会删除设备。

共同安装程序不能尝试中删除该设备本身通过调用**SetupDiRemoveDevice**。 共同安装程序通常处理此请求中后续处理之后已成功删除该设备。

如果共同安装程序必须删除注册表中的信息，例如，以便在后续处理，并且只当上一安装程序已成功删除请求共同安装程序应将执行操作。 在预处理传递，共同安装程序应将注册表信息存储在其上下文参数和返回 ERROR_DI_POSTPROCESSING_REQUIRED 请求后续处理。 当 Windows 调用共同安装程序的此差异请求的后续处理时，辅助安装程序应检查 DIF 状态是 NO_ERROR，然后删除注册表信息。 如果共同安装程序会删除其预处理阶段中的注册表信息和类安装程序 （或另一个辅助安装程序） 失败 DIF_REMOVE，辅助安装程序无法在不可预测的状态使该设备。

安装程序不应删除文件时处理此 DIF 请求，如果文件正在使用的另一台设备。

Windows 之前启动即插即用的查询删除会将发送此 DIF 请求，并删除处理。

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


[**SetupDiRemoveDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

[**SP_REMOVEDEVICE_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_removedevice_params)

 

 






