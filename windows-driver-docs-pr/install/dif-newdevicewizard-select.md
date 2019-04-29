---
title: DIF_NEWDEVICEWIZARD_SELECT
description: DIF_NEWDEVICEWIZARD_SELECT
ms.assetid: b6b2eaf7-c87f-45d6-8845-6d03bde9a802
keywords:
- DIF_NEWDEVICEWIZARD_SELECT 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_NEWDEVICEWIZARD_SELECT
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0192df62d3d4840b46116800ae07a47b00eb9d24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378372"
---
# <a name="difnewdevicewizardselect"></a>DIF_NEWDEVICEWIZARD_SELECT


DIF_NEWDEVICEWIZARD_SELECT 请求可让安装程序提供替换标准的选择驱动程序页的自定义向导页。 在手动安装的非 PnP 设备期间，才使用此请求。

### <a name="when-sent"></a>发送时间

之前 Windows 将显示"选择设备驱动程序"页。

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
提供的句柄[设备信息集](https://msdn.microsoft.com/library/windows/hardware/ff541247)，其中包含该设备。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
提供一个指向[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)标识设备中设备的信息集的结构。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)) 与关联*DeviceInfoData*。

<a href="" id="class-installation-parameters"></a>类的安装参数  
[ **SP_NEWDEVICEWIZARD_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff553305)与关联结构*DeviceInfoData*。

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改中设备安装参数的标志。 Windows 不会检查此 DIF 请求完成后的标志。 但是，它会检查它们在安装过程中更高版本。

<a href="" id="class-installation-parameters"></a>类的安装参数  
安装程序可以修改[ **SP_NEWDEVICEWIZARD_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff553305)提供自定义页面。

### <a name="installer-return-value"></a>安装程序返回值

如果共同安装程序不处理此 DIF 请求会返回 NO_ERROR 从其预处理阶段。 如果共同安装程序将处理此请求它可以返回 NO_ERROR、 ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

类安装程序返回 NO_ERROR，如果它已成功提供页面。 否则，类安装程序将返回 ERROR_DI_DO_DEFAULT 或 Win32 错误代码。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

DIF_NEWDEVICEWIZARD_SELECT 请求可让安装程序提供替换标准的选择驱动程序页的自定义向导页。 在手动安装的非 PnP 设备期间，才使用此请求。

安装程序响应此 DIF 请求彻底替换标准选择驱动程序向导页。 如果，相反，安装程序仅有修改标准的页或修改可供选择的驱动程序的列表，安装程序应该这样做以响应[ **DIF_SELECTDEVICE** ](dif-selectdevice.md)请求。

辅助安装程序应将添加自定义页面中其后续处理阶段且仅当类安装程序未将添加自定义页面。 如果类安装程序添加页面，辅助安装程序不应。 否则，可能会要求用户两次选择一个驱动程序。

如果安装程序提供自定义选择页上，安装程序必须设置所选驱动程序。 安装程序的代码中的向导页上，支持用户单击后**下一步**，安装程序必须调用[ **SetupDiSetSelectedDriver**](https://msdn.microsoft.com/library/windows/hardware/ff552183)。

安装程序应提供 Wizard 97 标头标题和自定义向导页的 PROPSHEETPAGE 结构中的标头副标题。 安装程序不应取代系统提供向导标题。 请参阅 Microsoft Windows SDK for PROPSHEETPAGE 结构的文档和有关属性页的详细信息。

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


[**DIF_NEWDEVICEWIZARD_PREANALYZE**](dif-newdevicewizard-preanalyze.md)

[**DIF_NEWDEVICEWIZARD_PRESELECT**](dif-newdevicewizard-preselect.md)

[**DIF_NEWDEVICEWIZARD_POSTANALYZE**](dif-newdevicewizard-postanalyze.md)

[**DIF_SELECTDEVICE**](dif-selectdevice.md)

[**SetupDiSetSelectedDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552176)

[**SetupDiSetSelectedDriver**](https://msdn.microsoft.com/library/windows/hardware/ff552183)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

[**SP_NEWDEVICEWIZARD_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff553305)

 

 






