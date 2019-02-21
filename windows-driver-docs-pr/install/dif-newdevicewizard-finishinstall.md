---
title: DIF_NEWDEVICEWIZARD_FINISHINSTALL
description: DIF_NEWDEVICEWIZARD_FINISHINSTALL
ms.assetid: 5d27316b-4e47-4e18-95fe-fd4a63a76626
keywords:
- DIF_NEWDEVICEWIZARD_FINISHINSTALL 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_NEWDEVICEWIZARD_FINISHINSTALL
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f272a415e87897329478a41594780f7c6b3f7a9a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525016"
---
# <a name="difnewdevicewizardfinishinstall"></a>DIF_NEWDEVICEWIZARD_FINISHINSTALL


DIF_NEWDEVICEWIZARD_FINISHINSTALL 请求可让安装程序提供 Windows 安装设备后向用户显示的完成安装向导页，但标准 Windows 显示之前完成页。 Windows 将发送此请求，以及管理员使用它安装即插即用 (PnP) 设备时**添加硬件向导**安装非 PnP 设备。

### <a name="when-sent"></a>发送时间

Windows 安装设备后 (在成功完成[ **DIF_INSTALLDEVICE** ](dif-installdevice.md)处理)，但然后再显示完成向导页。

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
句柄[设备信息集](https://msdn.microsoft.com/library/windows/hardware/ff541247)，其中包含该设备。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
一个指向[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)标识设备中设备的信息集的结构。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)) 与关联*DeviceInfoData*。

<a href="" id="class-installation-parameters"></a>类的安装参数  
[ **SP_NEWDEVICEWIZARD_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff553305)与关联结构*DeviceInfoData*。

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改中设备安装参数的标志。

<a href="" id="class-installation-parameters"></a>类的安装参数  
安装程序可以修改 SP_NEWDEVICEWIZARD_DATA 结构以提供完成安装向导页。

### <a name="installer-return-value"></a>安装程序返回值

如果共同安装程序不处理此 DIF 请求，辅助安装程序将返回 NO_ERROR 从其预处理阶段。 如果共同安装程序将处理此请求，辅助安装程序可以返回 NO_ERROR、 ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

类安装程序返回 NO_ERROR，如果安装程序已成功提供页面。 否则，类安装程序将返回 ERROR_DI_DO_DEFAULT 或 Win32 错误代码。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

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


[**DIF_FINISHINSTALL_ACTION**](dif-finishinstall-action.md)

[**DIF_INSTALLDEVICE**](dif-installdevice.md)

[**SetupDiChangeState**](https://msdn.microsoft.com/library/windows/hardware/ff550930)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

[**SP_NEWDEVICEWIZARD_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff553305)

 

 






