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
ms.openlocfilehash: 0d697517464b122e2c4b2e9adc86af0b1ff783ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524365"
---
# <a name="difallowinstall"></a>DIF_ALLOW_INSTALL


DIF_ALLOW_INSTALL 请求会为设备的安装程序要求 Windows 可以继续进行安装该设备。

### <a name="when-sent"></a>发送时间

后选择设备，但在安装设备之前的驱动程序。

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
提供的句柄[设备信息集](https://msdn.microsoft.com/library/windows/hardware/ff541247)，其中包含该设备。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
提供一个指向[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)标识设备中设备的信息集的结构。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)) 与关联*DeviceInfoData*。

<a href="" id="class-installation-parameters"></a>类的安装参数  
无

### <a name="installer-output"></a>安装程序输出

<a href="" id="none"></a>无  

### <a name="installer-return-value"></a>安装程序返回值

辅助安装程序可以返回 NO_ERROR 或 Win32 错误。 辅助安装程序不应返回 ERROR_DI_POSTPROCESSING_REQUIRED 此 DIF 请求。

类安装程序通常返回 ERROR_DI_DO_DEFAULT 或 Win32 错误代码。

典型的 Win32 错误代码，此差异请求包括 ERROR_DI_DONT_INSTALL 和 ERROR_NON_WINDOWS_NT_DRIVER。

**请注意**  类安装程序和共同安装程序应不 freturn ERROR_REQUIRES_INTERACTIVE_WINDOWSTATION，因为这将导致设备安装失败。 如果设备安装需要用户交互，类安装程序并共同安装程序应支持[完成安装操作](https://msdn.microsoft.com/library/windows/hardware/ff544940)。

 

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

在对 DIF_ALLOW_INSTALL 请求响应安装程序确认 Windows 是否可以安装该设备。

如果确定 （例如，如果该驱动程序是一个基于 NT 的操作系统将无法正常工作的 Windows 9 x 限驱动程序） 所选驱动程序是不正确或它将确定所选驱动程序已知有 bug，安装程序可能会失败此请求。

如果设备安装参数设置了 DI_QUIETINSTALL 标志和安装程序必须在设备安装过程中显示 UI，安装程序可能会失败此请求。 但是，此失败是罕见，因为安装程序通常提供响应 DIF_NEWDEVICEWIZARD_FINISHINSTALL 请求任何 UI 页。 在这种情况下，UI 不会阻止安装程序成功 DIF_ALLOW_INSTALL 请求为其设置 quiet 标志。 但是，如果安装程序不能限制其用户界面，以完成安装情况下，安装程序必须此 DIF 请求如果 DI_QUIETINSTALL 标志设置失败。 安装程序可能具有此限制，例如，如果它调用供应商提供的代码显示 UI。

如果安装程序失败此 DIF 请求，Windows 将停止安装。

如果此 DIF 请求失败的安装程序和设备的安装参数中未设置 DI_QUIETINSTALL，安装程序应显示一个对话框，并显示消息，解释了为什么不在安装设备。

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
<td align="left"><p>标头</p></td>
<td align="left">Setupapi.h （包括 Setupapi.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

 

 






