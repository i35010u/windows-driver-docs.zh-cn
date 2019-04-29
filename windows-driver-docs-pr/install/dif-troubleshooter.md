---
title: DIF_TROUBLESHOOTER
description: DIF_TROUBLESHOOTER
ms.assetid: e8477d4d-cc81-48aa-9d51-9f37c3cce0cb
keywords:
- DIF_TROUBLESHOOTER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_TROUBLESHOOTER
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a8e26cffb01fc59273548eaf3f455b4b0e8fd368
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365856"
---
# <a name="diftroubleshooter"></a>DIF_TROUBLESHOOTER


DIF_TROUBLESHOOTER 请求可让安装程序以启动设备故障排除工具，或返回 Windows 启动的 CHM 和 HTM 故障排除程序文件。

**请注意**  在 Windows Server 2003、 Windows XP 和 Microsoft Windows 2000 才支持此差异的代码。

 

### <a name="when-sent"></a>发送时间

当用户单击设备在设备管理器的"疑难解答"按钮。

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
[ **SP_TROUBLESHOOTER_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553341)与关联结构*DeviceInfoData*。

### <a name="installer-output"></a>安装程序输出

<a href="" id="class-installation-parameters"></a>类的安装参数  
安装程序可能会修改[ **SP_TROUBLESHOOTER_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553341)，设置 CHM 或 HTML 文件。

### <a name="installer-return-value"></a>安装程序返回值

如果共同安装程序不处理此请求，则返回 NO_ERROR 从其预处理阶段。

如果共同安装程序处理此请求，它会在后续处理传递。 如果共同安装程序提供 CHM 和 HTML 文件，它可传播收到 (可能 ERROR_DI_DO_DEFAULT) 的状态。 如果共同安装程序在运行疑难解答并解决问题，共同安装程序将返回 NO_ERROR。 如果共同安装程序在运行故障排除程序，但仍然无法解决问题，它可传播收到 (ERROR_DI_DO_DEFAULT) 的状态。

如果类安装程序提供的 CHM 文件和 HTML 文件，或类安装程序在运行故障排除程序，但仍然无法解决问题，类安装程序将返回 ERROR_DI_DO_DEFAULT。 随后，Windows 将调用默认处理程序。

如果类安装程序将启动其自己的故障排除并解决问题，类安装程序将返回 NO_ERROR。 Windows 将不会随后调用默认处理程序。

如果类安装程序遇到错误，安装程序将返回相应的 Win32 错误代码。 Windows 将不会随后调用默认处理程序。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

无

DIF_TROUBLESHOOTER，没有默认处理程序，但操作系统提供了默认尝试解决设备问题，如果没有安装程序提供故障排除程序的故障排除程序。

### <a name="installer-operation"></a>安装程序操作

安装程序将调用[ **CM_Get_DevNode_Status** ](https://msdn.microsoft.com/library/windows/hardware/ff538514)若要获取设备状态和 CM 问题的代码。 具体取决于问题，安装程序可能会提供疑难解答人员、 帮助文件，或执行任何操作。 疑难解答人员可能可以解决与设备的问题。 如果疑难解答人员可以解决此问题，则应调用**SetupDiCallClassInstaller**发送类型 DICS_PROPCHANGE DIF_PROPERTYCHANGE 请求。 如果安装程序不提供设备故障排除工具，它可能提供的解决问题的帮助文件的用户的建议。

如果没有安装程序在运行其自己的故障排除程序，Windows 将运行以向用户显示信息的 HTML 帮助。 如果安装程序提供的 CHM 文件中类安装参数，Windows 将显示该文件。 否则，Windows 将显示系统提供的疑难解答信息。

类安装参数最多包含**ChmFile**并**HtmlTroubleShooter**对。 如果多个安装程序指定这些值，Windows 将使用的最后一个安装程序处理 DIF 请求设置的值。

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
<td align="left"><p>支持 Windows Server 2003、 Windows XP 和 Microsoft Windows 2000 中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Setupapi.h （包括 Setupapi.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**CM_Get_DevNode_Status**](https://msdn.microsoft.com/library/windows/hardware/ff538514)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

[**SP_TROUBLESHOOTER_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553341)

 

 






