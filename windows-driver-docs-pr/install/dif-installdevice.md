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
ms.openlocfilehash: fd855b8253a0c0e4b642bd7155b622fa48c870dd
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361567"
---
# <a name="dif_installdevice"></a>DIF_INSTALLDEVICE


DIF_INSTALLDEVICE 请求允许安装程序在安装设备之前和/或之后执行任务。

### <a name="when-sent"></a>发送时间

选择驱动程序后，注册任何设备共同安装程序，并注册任何设备接口。

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
提供包含要安装的设备的 [设备信息集](./device-information-sets.md) 的句柄。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
在设备信息集中提供设备的 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
与 *DeviceInfoData* 关联的设备安装参数 ( [**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)) 。

<a href="" id="class-installation-parameters"></a>类安装参数  
None

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改 *DeviceInfoData* 的设备安装参数。 例如，安装程序可能会设置 DI_NEEDREBOOT 标志，或者它可能会设置 DI_DONOTCALLCONFIGMG 标志，以防止 Windows 使用新安装的驱动程序和设置动态地使设备联机。

### <a name="installer-return-value"></a>安装程序返回值

共同安装程序通常返回 NO_ERROR 或 ERROR_DI_POSTPROCESSING_REQUIRED。 共同安装程序也可能返回 Win32 错误代码。

如果类安装程序成功处理此请求，并且 [**SetupDiCallClassInstaller**](/windows/win32/api/setupapi/nf-setupapi-setupdicallclassinstaller) 随后应调用默认处理程序，则类安装程序将返回 ERROR_DI_DO_DEFAULT。

如果类安装程序成功处理此请求（包括直接调用默认处理程序），则类安装程序应返回 NO_ERROR 并且 **SetupDiCallClassInstaller** 将不会再次调用默认处理程序。

**注意**   类安装程序可以直接调用默认处理程序，但类安装程序永远不会尝试取代默认处理程序的操作。 有关调用默认的 DIF 代码处理程序的详细信息，请参阅 [调用默认的 Dif 代码处理程序](./calling-the-default-dif-code-handlers.md)。

 

如果类安装程序遇到错误，则安装程序应返回相应的 Win32 错误代码，并且 **SetupDiCallClassInstaller** 将不会随后调用默认处理程序。

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

[**SetupDiInstallDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdiinstalldevice)

### <a name="installer-operation"></a>安装程序操作

在响应 DIF_INSTALLDEVICE 请求时，安装程序通常会在默认的处理程序安装设备之前执行任何最终安装操作。 例如，安装程序可以检查注册表中所列设备的筛选器驱动程序和筛选器驱动程序和筛选器驱动程序和筛选器的筛选器。

除非在设备安装参数中设置了 DI_NOFILECOPY 标志，否则处理此 DIF 请求的安装程序应复制设备所需的文件，如驱动程序文件和控制面板文件。

如果 DI_NOFILECOPY 标志清晰但设置了 DI_NOVCP 标志，则安装程序必须将任何文件操作排队到提供的文件队列中，但不得提交队列。

共同安装程序可以在其预处理过程中处理此 DIF 请求，还可以在其后处理传递中处理此请求。 在预处理过程中，共同安装程序将执行 Windows 加载驱动程序和启动设备之前必须发生的所有操作。

在其后处理过程中，除非设置了 DI_NEEDREBOOT 标志，否则设备将启动并运行。 如果设置了此标志，Windows 将无法动态使设备联机。

如果安装程序返回 Win32 错误代码，Windows 会放弃安装。

如果 Windows 无法找到新设备的 INF 文件，则会发送 DIF_INSTALLDEVICE，尝试安装 *null 驱动程序* 。  ( [**SetupDiInstallDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdiinstalldevice) 的默认处理程序) 检查设备是否支持 *raw 模式* ，或是 [**IoReportDetectedDevice**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)) 报告的非 PnP 设备 (，在后一种情况下，Windows 将为设备安装 null 驱动程序。

如果此尝试失败，则 Windows 将再次发送 DIF_INSTALLDEVICE，这次在 [**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a) 结构中设置了 DI_FLAGSEX_SETFAILEDINSTALL 标志。 在这种情况下，默认处理程序只是在设备的 **ConfigFlags** 注册表值中设置 FAILEDINSTALL 标志。 如果设置了 DI_FLAGSEX_SETFAILEDINSTALL 标志，则类安装程序必须返回 NO_ERROR 或 ERROR_DI_DO_DEFAULT 并且共同安装程序必须返回 NO_ERROR。

有关 DIF 代码的详细信息，请参阅 [处理 Dif 代码](./handling-dif-codes.md)。

### <a name="calling-the-default-handler-setupdiinstalldevice"></a>**调用默认处理程序 SetupDiInstallDevice**

有关何时以及如何调用 **SetupDiInstallDevice** 的常规信息，请参阅 [调用默认的 DIF 代码处理程序](./calling-the-default-dif-code-handlers.md)。

在极少数情况下，如果类安装程序必须在所有 **SetupDiInstallDevice** 操作（启动设备除外）之后执行操作，则类安装程序必须：

1.  在调用 **SetupDiInstallDevice** 之前，请执行必须完成的操作。

2.  设置 SP_DEVINSTALL_PARAMS 中的 DI_DONOTCALLCONFIGMGR 标志。设备的 **标志** 成员。 如果设置了此标志，则 **SetupDiInstallDevice** 将执行除启动设备之外的所有默认安装操作。

3.  调用 **SetupDiInstallDevice** 以执行除启动设备之外的所有默认安装操作。

4.  执行所有默认安装操作（启动设备除外）完成后必须执行的操作。

5.  调用 [**SetupDiRestartDevices**](/windows/win32/api/setupapi/nf-setupapi-setupdirestartdevices) 启动设备。

6.  如果类安装程序成功完成安装操作或在安装操作失败时返回 Win32 错误，则返回 NO_ERROR。

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
<td align="left"><p>在 Microsoft Windows 2000 和更高版本的 Windows 中受支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Setupapi.log (包含 Setupapi.log) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DIF_INSTALLDEVICEFILES**](dif-installdevicefiles.md)

[**SetupDiInstallDevice**](/windows/win32/api/setupapi/nf-setupapi-setupdiinstalldevice)

[**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

