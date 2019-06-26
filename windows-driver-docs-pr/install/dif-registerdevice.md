---
title: DIF_REGISTERDEVICE
description: DIF_REGISTERDEVICE
ms.assetid: cb5f12f4-d429-4f02-b560-08807ffa3793
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
ms.openlocfilehash: 0e7c659ae9263048f0e964cc8897af235e6efb4b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386898"
---
# <a name="difregisterdevice"></a>DIF_REGISTERDEVICE


DIF_REGISTERDEVICE 请求可让安装程序以加入新创建的设备实例注册到的即插即用的管理器。 Windows 将发送非 PnP 设备的此差异请求。

### <a name="when-sent"></a>发送时间

当安装程序报告了以前未知的设备响应[ **DIF_DETECT** ](dif-detect.md)请求。 安装设备之前，Windows 将分析阶段的添加硬件向导中发送此 DIF 请求。 Windows 在非 PnP 检测过程还会发送此请求。

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
提供的句柄[设备信息集](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)，其中包含该设备。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
提供一个指向[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)标识设备中设备的信息集的结构。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) 与关联*DeviceInfoData*。

<a href="" id="class-installation-parameters-"></a>类的安装参数   
无

### <a name="installer-output"></a>安装程序输出

无

### <a name="installer-return-value"></a>安装程序返回值

辅助安装程序可以返回 NO_ERROR 或 Win32 错误代码。 辅助安装程序不应返回 ERROR_DI_POSTPROCESSING_REQUIRED 此 DIF 请求。

如果安装程序确定是否返回 ERROR_DUPLICATE_FOUND 重复设备。

如果类安装程序已成功处理此请求并[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)应随后调用默认处理程序类安装程序将返回 ERROR_DI_DO_DEFAULT。

类安装程序类安装程序将成功处理此请求，包括直接调用默认处理程序，如果应返回 NO_ERROR 并**SetupDiCallClassInstaller**随后不会调用默认处理程序电子邮件了。

**请注意**  类安装程序可以直接调用默认处理程序，但类安装程序应永远不会尝试取代默认处理程序的操作。

 

调用默认处理程序的详细信息，请参阅[调用默认 DIF 代码处理程序](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)。

安装程序类安装程序遇到错误，如果应返回相应的 Win32 错误代码和**SetupDiCallClassInstaller**随后不会调用默认处理程序。

如果安装程序确定设备重复，安装程序将返回 ERROR_DUPLICATE_FOUND。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

[**SetupDiRegisterDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)

### <a name="installer-operation"></a>安装程序操作

一个*设备安装应用程序*通常情况下发送此差异的请求向即插即用注册非 PnP 设备管理器。 从 Microsoft Windows 2000 开始，非 PnP 设备必须注册然后才能安装它们。

安装程序通常会处理此差异的请求执行重复检测。 此类安装程序通常会调用默认处理程序 ([**SetupDiRegisterDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo))，并指定其检测例程。 如果注册成功，并且安装程序确定设备不重复，安装程序将返回 NO_ERROR。

辅助安装程序应执行任何操作来处理在预处理传递此 DIF 请求。 辅助安装程序的后续处理调用时，通过类安装程序或默认处理程序已注册的设备实例。

如果安装程序将返回此 DIF 代码错误，通常 ERROR_DUPLICATE_FOUND，Windows 删除设备中设备的信息集。

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


[**DIF_DETECT**](dif-detect.md)

[**SetupDiRegisterDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






