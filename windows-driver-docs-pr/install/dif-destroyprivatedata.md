---
title: DIF_DESTROYPRIVATEDATA
description: DIF_DESTROYPRIVATEDATA
keywords:
- DIF_DESTROYPRIVATEDATA 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_DESTROYPRIVATEDATA
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b93712b453fb98e1e153b6663a75a5b836e11908
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832965"
---
# <a name="dif_destroyprivatedata"></a>DIF_DESTROYPRIVATEDATA


DIF_DESTROYPRIVATEDATA 请求指示类安装程序释放它所分配的或存储在 [**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)结构的 **ClassInstallReserved** 字段中的任何内存或资源。

### <a name="when-sent"></a>发送时间

当 Windows 销毁 [设备信息集](./device-information-sets.md) 或 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 元素时，或在 windows 丢弃设备的共同安装程序和类安装程序列表时。

### <a name="who-handles"></a>谁处理

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>类共同安装程序</p></td>
<td align="left"><p>不处理</p></td>
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
提供设备信息集的句柄。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
还可以提供一个指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构在设备信息集中标识设备。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a))  (设备安装参数与 *DeviceInfoData*（如果已指定）或与 *DeviceInfoSet* 相关联。

<a href="" id="class-installation-parameters"></a>类安装参数  
无

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters-"></a>设备安装参数   
安装程序可以 ([**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)) 中清除设备安装参数中的 **ClassInstallReserved** 字段。

### <a name="installer-return-value"></a>安装程序返回值

共同安装程序不处理此 DIF 请求。 它只会在其预处理传递中返回 NO_ERROR。

类安装程序通常返回 ERROR_DI_DO_DEFAULT 或 Win32 错误代码。

### <a name="default-dif-code-handler"></a>默认的 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

为响应 DIF_DESTROYPRIVATEDATA 请求，类安装程序将释放它所分配的任何内存或资源，并将其存储在 [**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)结构的 **ClassInstallReserved** 字段中。

共同安装程序不应使用 **ClassInstallReserved** 字段。

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

## <a name="see-also"></a>请参阅


[**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

 

