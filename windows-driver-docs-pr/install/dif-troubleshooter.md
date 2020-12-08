---
title: DIF_TROUBLESHOOTER
description: DIF_TROUBLESHOOTER
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
ms.openlocfilehash: a0bce5091b0ce12d8ce69d68951b119cacffdbac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840351"
---
# <a name="dif_troubleshooter"></a>DIF_TROUBLESHOOTER


DIF_TROUBLESHOOTER 请求允许安装程序为设备启动疑难解答，或返回 CHM 和 HTM 疑难解答文件以使 Windows 启动。

**注意**  此 DIF 代码仅在 Windows Server 2003、Windows XP 和 Microsoft Windows 2000 上受支持。

 

### <a name="when-sent"></a>发送时间

当用户在设备管理器中单击设备的 "疑难解答" 按钮时。

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
提供包含设备的 [设备信息集](./device-information-sets.md) 的句柄。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
提供一个指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构在设备信息集中标识设备。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
与 *DeviceInfoData* 关联的设备安装参数 ([**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)) 。

<a href="" id="class-installation-parameters"></a>类安装参数  
[**SP_TROUBLESHOOTER_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_troubleshooter_params_a)结构与 *DeviceInfoData* 关联。

### <a name="installer-output"></a>安装程序输出

<a href="" id="class-installation-parameters"></a>类安装参数  
安装程序可能会修改 [**SP_TROUBLESHOOTER_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_troubleshooter_params_a)、设置 CHM 或 HTML 文件。

### <a name="installer-return-value"></a>安装程序返回值

如果联合安装程序不处理此请求，它将从其预处理传递返回 NO_ERROR。

如果共同安装程序处理此请求，它会在其后处理过程中执行此操作。 如果共同安装程序提供了 CHM 和 HTML 文件，它将传播收到的状态， (可能 ERROR_DI_DO_DEFAULT 的) 。 如果共同安装程序运行疑难解答程序并修复问题，则共同安装程序将返回 NO_ERROR。 如果共同安装程序运行疑难解答，但没有解决问题，它会将收到的状态传播 (ERROR_DI_DO_DEFAULT) 。

如果类安装程序提供了 CHM 文件和 HTML 文件，或者类安装程序运行了疑难解答程序但不能解决问题，则类安装程序将返回 ERROR_DI_DO_DEFAULT。 然后，Windows 将调用默认处理程序。

如果类安装程序启动其自己的疑难解答并修复了问题，则类安装程序将返回 NO_ERROR。 然后，Windows 将不会调用默认处理程序。

如果类安装程序遇到错误，安装程序将返回相应的 Win32 错误代码。 然后，Windows 将不会调用默认处理程序。

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

无

DIF_TROUBLESHOOTER 没有默认的处理程序，但是，如果没有安装程序提供程序的疑难解答程序，操作系统会提供默认的疑难解答程序来尝试解决设备问题。

### <a name="installer-operation"></a>安装程序操作

安装程序调用 [**CM_Get_DevNode_Status**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status) 以获取设备状态和 CM 问题代码。 根据具体的问题，安装程序可能会提供疑难解答、帮助文件或任何内容。 疑难解答可能会解决设备问题。 如果疑难解答解决了问题，则它应调用 **SetupDiCallClassInstaller** 以发送 DICS_PROPCHANGE 类型的 DIF_PROPERTYCHANGE 请求。 如果安装程序未提供设备的疑难解答，则可能会为用户提供问题解决建议的帮助文件。

如果没有安装程序运行自己的疑难解答，Windows 将运行 HTML 帮助向用户显示信息。 如果安装程序在类安装参数中提供了 CHM 文件，则 Windows 将显示该文件。 否则，Windows 将显示系统提供的故障排除信息。

类安装参数最多包含一个 **ChmFile** 和 **HtmlTroubleShooter** 对。 如果多个安装程序指定了这些值，则 Windows 将使用由处理该 DIF 请求的上一个安装程序设置的值。

有关 DIF 代码的详细信息，请参阅 [处理 Dif 代码](./handling-dif-codes.md)。

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
<td align="left"><p>在 Windows Server 2003、Windows XP 和 Microsoft Windows 2000 中受支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Setupapi.log (包含 Setupapi.log) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**CM_Get_DevNode_Status**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)

[**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

[**SP_TROUBLESHOOTER_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_troubleshooter_params_a)

 

