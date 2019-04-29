---
title: DIF_FIRSTTIMESETUP
description: DIF_FIRSTTIMESETUP
ms.assetid: 6ac4da58-3f4f-4fcd-96e2-c480975159e0
keywords:
- DIF_FIRSTTIMESETUP 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_FIRSTTIMESETUP
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 126beeec9ae35cbefa9e6a2aacb58fbfa8b344b9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362781"
---
# <a name="diffirsttimesetup"></a>DIF_FIRSTTIMESETUP


此差异代码保留供系统使用。 供应商提供的安装程序必须处理此请求，除非在供应商提供的安装程序必须检测到非 PnP 设备。

DIF_FIRSTTIMESETUP 请求指示安装程序来执行必须在操作系统的初始安装过程中完成的任何特定于类的安装任务。

### <a name="when-sent"></a>发送时间

在 GUI 模式下安装程序。

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
提供的句柄的设备信息设置。 没有[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)与关联*DeviceInfoSet*。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
无

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)) 与关联*DeviceInfoSet*。

<a href="" id="class-installation-parameters"></a>类的安装参数  
无

### <a name="installer-output"></a>安装程序输出

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
安装程序将添加到的设备信息元素*DeviceInfoSet*为每个检测到它想要安装的设备。 安装程序还可能会生成一个全局类驱动程序列表。

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改的设备安装参数*DeviceInfoSet*或为其创建的新设备信息元素。

### <a name="installer-return-value"></a>安装程序返回值

类共同安装程序可以在预处理或后处理过程中检测到设备。 此类共同安装程序 （适用于后续处理） 返回 ERROR_DI_POSTPROCESSING_REQUIRED 和/或其检测操作之后，返回 NO_ERROR 或 Win32 错误代码。 如果共同安装程序不会检测设备，则返回 NO_ERROR 从其预处理阶段。

如果类安装程序检测到设备时，安装程序将返回 NO_ERROR 或相应的 Win32 错误代码。 如果类安装程序不处理此 DIF 请求，安装程序将返回 ERROR_DI_DO_DEFAULT。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

若要在 GUI 模式下安装过程中检测到非 PnP 设备，安装程序必须处理 DIF_FIRSTTIMESETUP 请求。 GUI 模式下安装程序不会发送[ **DIF_DETECT** ](dif-detect.md)到安装程序的请求。

GUI 模式下安装程序将发送一个空的 DIF_FIRSTTIMESETUP 请求*DeviceInfoSet*。 安装程序可以执行非 PnP 设备的旧检测并将其添加到*DeviceInfoSet*。 从 Windows 9 迁移旧的设备安装时，系统提供的安装程序还可以处理此 DIF 请求 x / Me 或 Windows NT 到 Microsoft Windows 2000 和更高版本的 Windows。

安装程序检测到基于注册表的信息，通过调入内核模式检测组件，或通过咨询其安装程序类的新设备*unattend.txt*迁移期间运行的 DLL 时存储的信息操作系统升级。

安装程序安装程序检测到非 PnP 设备，如果应按如下所示选择设备的驱动程序： 创建设备信息元素 ([**SetupDiCreateDeviceInfo**](https://msdn.microsoft.com/library/windows/hardware/ff550952))，设置 SPDRP_HARDWAREID通过调用[ **SetupDiSetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552169)，调用[ **SetupDiBuildDriverInfoList**](https://msdn.microsoft.com/library/windows/hardware/ff550917)，然后调用[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)发送[ **DIF_SELECTBESTCOMPATDRV** ](dif-selectbestcompatdrv.md)请求。

如果一个或多个安装程序检测到此 DIF 代码的响应中的设备，GUI 模式下安装程序将尝试安装设备。 GUI 模式下安装程序将尝试在列表中; 安装所有设备如果安装程序返回以前配置的设备，GUI 模式下安装程序将两次安装该设备。

安装程序必须以无提示方式处理此差异的请求。 也就是说，而不会向用户显示 UI。

安装程序不应执行的任务在其处理要求计算机重新启动此 DIF 请求。 例如，类安装程序不应设置在下次启动时用于确定哪些驱动程序成功完成后重新启动时加载的驱动程序。

若要在 GUI 模式下安装过程中检测到非 PnP 设备，安装程序必须处理此请求。 GUI 模式下安装程序不发送 DIF_DETECT 请求。

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


[**DIF_SELECTBESTCOMPATDRV**](dif-selectbestcompatdrv.md)

[**SetupDiBuildDriverInfoList**](https://msdn.microsoft.com/library/windows/hardware/ff550917)

[**SetupDiCallClassInstaller**](https://msdn.microsoft.com/library/windows/hardware/ff550922)

[**SetupDiCreateDeviceInfo**](https://msdn.microsoft.com/library/windows/hardware/ff550952)

[**SetupDiSetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552169)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

 

 






