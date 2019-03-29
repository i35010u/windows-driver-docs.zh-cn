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
ms.openlocfilehash: 080d5f2d7f57b2767cb02f683f1f56784b31db97
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562112"
---
# <a name="difpropertychange"></a>DIF_PROPERTYCHANGE


DIF_PROPERTYCHANGE 请求通知安装程序要更改设备的属性。 设备正在启用、 禁用、 启动，停止，或在属性页上的某些项已更改。 此差异请求使安装程序有机会参与更改。

### <a name="when-sent"></a>发送时间

当正在启用设备，已禁用，重新启动，停止，或者其属性已更改。

例如，Windows 会发送此请求时的属性页提供程序中设置 DI_FLAGSEX_PROPCHANGE_PENDING 标志**FlagsEx**字段[ **SP_DEVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552346)结构的设备。

有关检测设备是第一次启动或随后重新启动时的详细信息，请参阅安装程序操作部分。

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
提供的句柄[设备信息集](https://msdn.microsoft.com/library/windows/hardware/ff541247)，其中包含该设备。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
提供一个指向[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)设备中设备的信息集的结构。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)) 与关联*DeviceInfoData*。

<a href="" id="class-installation-parameters"></a>类的安装参数  
[ **SP_PROPCHANGE_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553315)与关联结构*DeviceInfoData*。

### <a name="installer-output"></a>安装程序输出

<a href="" id="none"></a>无  

### <a name="installer-return-value"></a>安装程序返回值

辅助安装程序可以返回 NO_ERROR、 ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

如果类安装程序已成功处理此请求并[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)应随后调用默认处理程序类安装程序将返回 ERROR_DI_DO_DEFAULT。

类安装程序类安装程序将成功处理此请求，包括直接调用默认处理程序，如果应返回 NO_ERROR 并**SetupDiCallClassInstaller**随后不会调用默认处理程序电子邮件了。

**请注意**  类安装程序可以直接调用默认处理程序，但类安装程序应永远不会尝试取代默认处理程序的操作。

 

调用默认处理程序的详细信息，请参阅[调用默认 DIF 代码处理程序](https://msdn.microsoft.com/library/windows/hardware/ff537868)。

安装程序类安装程序遇到错误，如果应返回相应的 Win32 错误代码和**SetupDiCallClassInstaller**随后不会调用默认处理程序。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

[**SetupDiChangeState**](https://msdn.microsoft.com/library/windows/hardware/ff550930)

### <a name="installer-operation"></a>安装程序操作

DIF_PROPERTYCHANGE 请求响应中安装程序可以参与属性更改操作。 类安装参数 (SP_PROPCHANGE_PARAMS) 指示哪些更改正在进行。

属性更改可能需要重新启动系统。 有关如何重新启动系统的信息，请参阅[ **SetupDiCallClassInstaller**](https://msdn.microsoft.com/library/windows/hardware/ff550922)。

当 Windows 发送 DIF_INSTALLDEVICE 请求第一次安装的设备时，Windows 将使设备开始，但不作为安装的一部分发送 DIF_PROPERTYCHANGE 请求。 如果第一次，只要随后重新启动设备启动设备时，必须执行自定义安装操作，安装程序或辅助安装程序应处理的 DIF_INSTALLDEVICE 请求的第一次启动设备和 DIF_PROPERTYCHANGE 请求，以指示状态更改操作正在启动设备。

有关差异代码的详细信息，请参阅[处理 DIF 代码](https://msdn.microsoft.com/library/windows/hardware/ff546094)。

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
<td align="left"><p>Microsoft Windows 2000 和更高版本的 Windows 支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Setupapi.h （包括 Setupapi.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**SetupDiChangeState**](https://msdn.microsoft.com/library/windows/hardware/ff550930)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

[**SP_PROPCHANGE_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553315)

 

 






