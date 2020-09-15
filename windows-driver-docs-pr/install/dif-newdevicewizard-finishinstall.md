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
ms.openlocfilehash: d041193c050f897b756ddb525470138a7217eb48
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107290"
---
# <a name="dif_newdevicewizard_finishinstall"></a>DIF_NEWDEVICEWIZARD_FINISHINSTALL


DIF_NEWDEVICEWIZARD_FINISHINSTALL 请求允许安装程序提供在设备安装之后但在 Windows 显示标准的 "完成" 页之前 Windows 向用户显示的 "完成安装向导" 页面。 当 Windows 安装即插即用 (PnP) 设备以及管理员使用 " **添加硬件向导** " 来安装非 PnP 设备时，Windows 将发送此请求。

### <a name="when-sent"></a>发送时间

Windows 安装设备后 ([**DIF_INSTALLDEVICE**](dif-installdevice.md) 处理) 成功完成，但在显示 "完成向导" 页面之前。

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
包含设备的 [设备信息集](./device-information-sets.md) 的句柄。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
一个指针，指向用于在设备信息集中标识设备的 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
与*DeviceInfoData*关联的设备安装参数 ([**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)) 。

<a href="" id="class-installation-parameters"></a>类安装参数  
[**SP_NEWDEVICEWIZARD_DATA**](/windows/desktop/api/setupapi/ns-setupapi-_sp_newdevicewizard_data)结构与*DeviceInfoData*关联。

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters"></a>设备安装参数  
安装程序可以修改设备安装参数中的标志。

<a href="" id="class-installation-parameters"></a>类安装参数  
安装程序可以修改 SP_NEWDEVICEWIZARD_DATA 结构以提供 "完成安装向导" 页面。

### <a name="installer-return-value"></a>安装程序返回值

如果共同安装程序不处理此 DIF 请求，则共同安装程序将从其预处理传递返回 NO_ERROR。 如果共同安装程序处理此请求，则共同安装程序可以返回 NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED 或 Win32 错误代码。

如果安装程序成功提供了页面，则类安装程序将返回 NO_ERROR。 否则，类安装程序将返回 ERROR_DI_DO_DEFAULT 或 Win32 错误代码。

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

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
<td align="left"><p>在 Microsoft Windows 2000 和更高版本的 Windows 中受支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Setupapi.log (包含 Setupapi.log) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**DIF_FINISHINSTALL_ACTION**](dif-finishinstall-action.md)

[**DIF_INSTALLDEVICE**](dif-installdevice.md)

[**SetupDiChangeState**](/windows/desktop/api/setupapi/nf-setupapi-setupdichangestate)

[**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

[**SP_NEWDEVICEWIZARD_DATA**](/windows/desktop/api/setupapi/ns-setupapi-_sp_newdevicewizard_data)

 

