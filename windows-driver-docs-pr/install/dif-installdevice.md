---
title: DIF_INSTALLDEVICE
description: DIF_INSTALLDEVICE
ms.assetid: 2d369086-c2b6-45a4-a87e-51ff5725938f
keywords:
- DIF_INSTALLDEVICE 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_INSTALLDEVICE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 120af0bf402cec8117556314c3855953f69f5dbd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566426"
---
# <a name="difinstalldevice"></a>DIF_INSTALLDEVICE


DIF_INSTALLDEVICE 请求可让安装程序之前/之后的设备安装或执行任务。

### <a name="when-sent"></a>发送时间

选择后，驱动程序，注册任何设备共同安装程序，并注册任何设备接口。

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
提供的句柄[设备信息集](https://msdn.microsoft.com/library/windows/hardware/ff541247)，其中包含要安装的设备。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
提供一个指向[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)设备中设备的信息集的结构。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)) 与关联*DeviceInfoData*。

<a href="" id="class-installation-parameters"></a>类的安装参数  
无

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改的设备安装参数*DeviceInfoData*。 例如，安装程序可能设置 DI_NEEDREBOOT 标志，或者它可能会设置 DI_DONOTCALLCONFIGMG 标志，以防止 Windows 自带设备联机动态使用其新安装的驱动程序和设置。

### <a name="installer-return-value"></a>安装程序返回值

辅助安装程序通常返回 NO_ERROR 或 ERROR_DI_POSTPROCESSING_REQUIRED。 辅助安装程序可能也会返回一个 Win32 错误代码。

如果类安装程序已成功处理此请求并[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)应随后调用默认处理程序类安装程序将返回 ERROR_DI_DO_DEFAULT。

类安装程序类安装程序将成功处理此请求，包括直接调用默认处理程序，如果应返回 NO_ERROR 并**SetupDiCallClassInstaller**随后不会调用默认处理程序电子邮件了。

**请注意**  类安装程序可以直接调用默认处理程序，但类安装程序应永远不会尝试取代默认处理程序的操作。 调用默认 DIF 代码处理程序的详细信息，请参阅[调用默认 DIF 代码处理程序](https://msdn.microsoft.com/library/windows/hardware/ff537868)。

 

安装程序类安装程序遇到错误，如果应返回相应的 Win32 错误代码和**SetupDiCallClassInstaller**随后不会调用默认处理程序。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

[**SetupDiInstallDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552039)

### <a name="installer-operation"></a>安装程序操作

DIF_INSTALLDEVICE 请求响应中安装程序通常执行的任何最终的安装操作的默认处理程序安装设备之前。 例如，安装程序可以检查，并可能修改的上限筛选器驱动程序和更低的筛选器驱动程序注册表中列出的设备。

除非设备安装参数中设置了 DI_NOFILECOPY 标志，安装程序以便处理此 DIF 请求应复制所需的设备，如驱动程序文件和控制面板文件的文件。

如果 DI_NOFILECOPY 标志已清除，但 DI_NOVCP 标志设置，安装程序必须排入队列到队列提供的文件的所有文件操作，但都必须提交队列。

辅助安装程序可以处理此 DIF 请求在预处理传递和/或其后续处理阶段中。 在其预处理阶段中，辅助安装程序执行 Windows 加载驱动程序，并使设备开始之前，必须执行任何操作。

在其后续处理阶段中，设备已启动并运行除非 DI_NEEDREBOOT 标志已设置。 如果设置此标志，Windows 不可能动态地将设备联机。

如果安装程序将返回 Win32 错误代码，Windows 将放弃安装。

如果 Windows 找不到新设备的 INF 文件，它在尝试安装发送 DIF_INSTALLDEVICE*为 null 的驱动程序*。 默认处理程序 (**SetupDiInstallDevice**或为非 PnP 设备 (由报告[ **IoReportDetectedDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549597))，在后一种情况下，Windows 安装的 null 驱动程序设备。

如果此尝试失败，Windows 将发送 DIF_INSTALLDEVICE 同样，这次使用 DI_FLAGSEX_SETFAILEDINSTALL 标志中设置[ **SP_DEVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552346)结构。 在这种情况下，默认处理程序只需 FAILEDINSTALL 中的标志设置的设备**配置标志**注册表值。 如果设置了 DI_FLAGSEX_SETFAILEDINSTALL 标志，类安装程序必须返回 NO_ERROR 或 ERROR_DI_DO_DEFAULT 和共同安装程序必须返回 NO_ERROR。

有关差异代码的详细信息，请参阅[处理 DIF 代码](https://msdn.microsoft.com/library/windows/hardware/ff546094)。

### <a name="calling-the-default-handler-setupdiinstalldevice"></a>**调用默认处理程序 SetupDiInstallDevice**

有关何时以及如何调用常规信息**SetupDiInstallDevice**，请参阅[调用默认的 DIF 代码处理程序](https://msdn.microsoft.com/library/windows/hardware/ff537868)。

在类安装程序必须毕竟执行操作的极少数情况下**SetupDiInstallDevice**已完成操作，但从一台设备，除外，类安装程序必须：

1.  执行之前调用都必须执行的操作**SetupDiInstallDevice**。

2.  设置在 SP_DEVINSTALL_PARAMS DI_DONOTCALLCONFIGMGR 标志。**标志**设备的成员。 如果设置此标志， **SetupDiInstallDevice**执行除启动设备的所有默认安装操作。

3.  调用**SetupDiInstallDevice**能够执行除了启动设备的所有默认安装操作。

4.  执行后完成所有的默认安装操作，除了启动设备，必须执行的操作。

5.  调用[ **SetupDiRestartDevices** ](https://msdn.microsoft.com/library/windows/hardware/ff552104)以启动设备。

6.  如果类安装程序已成功完成安装操作，则返回 NO_ERROR 或如果安装操作失败，则返回一个 Win32 错误。

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


[**DIF_INSTALLDEVICEFILES**](dif-installdevicefiles.md)

[**SetupDiInstallDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552039)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

 

 






