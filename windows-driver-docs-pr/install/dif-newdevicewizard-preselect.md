---
title: DIF_NEWDEVICEWIZARD_PRESELECT
description: DIF_NEWDEVICEWIZARD_PRESELECT
ms.assetid: 51aec9bf-11c1-4df9-bb44-0cfde066f73d
keywords:
- DIF_NEWDEVICEWIZARD_PRESELECT 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_NEWDEVICEWIZARD_PRESELECT
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1d0092b8d38ab0e70baac21e2c72fc44f0b16263
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543378"
---
# <a name="difnewdevicewizardpreselect"></a>DIF_NEWDEVICEWIZARD_PRESELECT


DIF_NEWDEVICEWIZARD_PRESELECT 请求可让安装程序提供向用户显示 Windows 然后再显示选择驱动程序页的向导页。 在手动安装的非 PnP 设备期间，才使用此请求。

### <a name="when-sent"></a>发送时间

用户所选设备的类之前后 Windows 将显示"选择设备驱动程序"页面。

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

DIF_NEWDEVICEWIZARD_PRESELECT 请求可让安装程序提供向用户显示 Windows 然后再显示选择驱动程序页的向导页。 在手动安装的非 PnP 设备期间，才使用此请求。

如果安装添加自定义预先选择页面，安装程序应首先检查是否**NumDynamicPages**类安装参数已达到 MAX_INSTALLWIZARD_DYNAPAGES。

在预处理传递和/或其后续处理阶段中，辅助安装程序可以添加自定义页。 如果在预处理传递添加页面，这些页面显示之前由类安装程序提供任何页面。

如果一个或多个安装程序添加自定义预先选择页面，Windows 将显示"选择设备驱动程序"页之前的页。 但是，如果用户按"上一步"，在选择驱动程序页上，Windows 将跳过自定义 preselect 页并返回到"硬件类型"类选择页面。

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


[**DIF_NEWDEVICEWIZARD_PREANALYZE**](dif-newdevicewizard-preanalyze.md)

[**DIF_NEWDEVICEWIZARD_POSTANALYZE**](dif-newdevicewizard-postanalyze.md)

[**DIF_NEWDEVICEWIZARD_SELECT**](dif-newdevicewizard-select.md)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

[**SP_NEWDEVICEWIZARD_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff553305)

 

 






