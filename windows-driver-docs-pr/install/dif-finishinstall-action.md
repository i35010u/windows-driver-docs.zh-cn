---
title: DIF_FINISHINSTALL_ACTION
description: DIF_FINISHINSTALL_ACTION
ms.assetid: 76eba79b-7a8a-478e-aaea-8b36eee51846
keywords:
- DIF_FINISHINSTALL_ACTION 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_FINISHINSTALL_ACTION
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e02bfec1d096df8beba1a25769260c9bf133ef20
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104286"
---
# <a name="dif_finishinstall_action"></a>DIF_FINISHINSTALL_ACTION


当所有其他设备安装操作完成后，DIF_FINISHINSTALL_ACTION 请求允许安装程序在交互式管理员上下文中运行 "完成-安装" 操作。

### <a name="when-sent"></a>发送时间

在 Windows 8 及更高版本中，"完成-安装" 操作不会在设备安装过程中自动运行。 若要完成设备完成安装操作，用户必须在操作中心单击 "完成安装设备软件" 以完成安装。

有关详细信息，请参阅 [运行完成-安装操作](./running-finish-install-actions.md)。

在 Windows 7 中，仅在以下时间之一使用管理员凭据在用户的上下文中运行完成安装过程：

-   下一次在附加设备时具有管理员凭据的用户登录的时间。
-   重新附加设备时。
-   当用户在设备管理器中选择 "扫描硬件更改" 时。

如果用户在没有管理权限的情况下登录，则 Windows 将提示用户提供许可和凭据，以便在管理员上下文中运行完成安装操作。

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
包含正在安装的设备的 [设备信息集](./device-information-sets.md) 的句柄。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
指向表示正在安装的设备的 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
与*DeviceInfoData*关联的[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)结构)  (有设备安装参数。

<a href="" id="class-installation-parameters"></a>类安装参数  
无

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters-"></a>设备安装参数   
如果需要重新启动系统才能完成其完成安装操作，安装程序将设置 DI_NEEDREBOOT 标志。

### <a name="installer-return-value"></a>安装程序返回值

安装程序返回下表中列出的值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ERROR_DI_DO_DEFAULT</p></td>
<td align="left"><p>类安装程序：安装程序没有完成安装操作，已成功完成完成安装操作，或已确定它无法成功完成其完成安装操作。 设备安装应执行请求的默认处理。</p>
<p>共同安装程序：共同安装程序不得返回此错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NO_ERROR</p></td>
<td align="left"><p>类安装程序：类安装程序不应返回此错误代码。 如果类安装程序返回此错误代码，则设备安装不会对该请求执行默认处理。</p>
<p>共同安装程序：安装程序没有完成安装操作，已成功完成完成安装操作，或已确定它无法成功完成其完成安装操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Win32 错误代码</p></td>
<td align="left"><p>类安装程序或共同安装程序：安装程序在处理完成安装操作时遇到错误，设备安装应在管理员的上下文中下次枚举设备时尝试完成完成安装操作。</p></td>
</tr>
</tbody>
</table>

 

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

Windows 7 使用 [**SetupDiFinishInstallAction**](/previous-versions/windows/hardware/previsioning-framework/ff551022(v=vs.85))。

Windows 8 及更高版本中没有默认的 DIF 代码处理程序，并且 [**SetupDiFinishInstallAction**](/previous-versions/windows/hardware/previsioning-framework/ff551022(v=vs.85)) 已被删除。

### <a name="comments"></a>注释

由于设备安装无法从 ERROR_DI_DO_DEFAULT 返回代码或 NO_ERROR 返回代码确定完成-安装操作是否确实成功，因此安装程序应通知用户完成安装程序操作的状态。

有关完成安装操作的详细信息，请参阅 [设备安装如何处理完成-安装操作](./how-finish-install-actions-are-processed.md) 和 [实现完成-安装操作](./implementing-finish-install-actions.md)。

有关 DIF 代码的常规信息，请参阅 [处理 Dif 代码](./handling-dif-codes.md) 和 [调用默认的 Dif 代码处理程序](./calling-the-default-dif-code-handlers.md)。

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
<td align="left"><p>在 Windows Vista 到 Windows 7 中受支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Setupapi.log (包含 Setupapi.log) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**SetupDiFinishInstallAction**](/previous-versions/windows/hardware/previsioning-framework/ff551022(v=vs.85))

 

