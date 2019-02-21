---
title: DIF_POWERMESSAGEWAKE
description: DIF_POWERMESSAGEWAKE
ms.assetid: 73f6e763-0900-4297-ac88-20bbb3ac424d
keywords:
- DIF_POWERMESSAGEWAKE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_POWERMESSAGEWAKE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3b5876c1de677d30d351f86d6fd0befef99a6f71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523868"
---
# <a name="difpowermessagewake"></a>DIF_POWERMESSAGEWAKE


DIF_POWERMESSAGEWAKE 请求可让安装程序提供自定义 Windows 的设备属性的电源管理属性页显示的文本。

### <a name="when-sent"></a>发送时间

当用户单击的菜单项或选项卡以显示设备的属性。

Windows 仅发送此 DIF 请求，如果设备的驱动程序支持电源管理。 否则，Windows 不显示任何设备的 power 属性。

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
提供一个指向[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)标识设备中设备的信息集的结构。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)) 与关联*DeviceInfoData*。

<a href="" id="class-installation-parameters"></a>类的安装参数  
[ **SP_POWERMESSAGEWAKE_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553311)与关联结构*DeviceInfoData*。

### <a name="installer-output"></a>安装程序输出

<a href="" id="class-installation-parameters"></a>类的安装参数  
安装程序可以修改[ **SP_POWERMESSAGEWAKE_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553311)提供设备的 power 属性页的自定义文本。

### <a name="installer-return-value"></a>安装程序返回值

辅助安装程序通常返回 NO_ERROR、 ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

类安装程序返回 NO_ERROR，如果它已成功提供 power 属性文本。 否则，类安装程序将返回 ERROR_DI_DO_DEFAULT 或 Win32 错误代码。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

DIF_POWERMESSAGEWAKE 请求可让安装程序提供 Windows 设备的 power 属性页显示的文本。

如果共同安装程序提供电源属性文本，它应在其后续处理阶段中实现。 辅助安装程序时应小心覆盖由处理请求之前共同安装程序的安装程序提供的任何电源属性文本。

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

[**SP_POWERMESSAGEWAKE_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553311)

 

 






