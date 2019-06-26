---
title: DIF_DESTROYPRIVATEDATA
description: DIF_DESTROYPRIVATEDATA
ms.assetid: 4f5d423d-52a5-4f7a-9847-b0e65b1c6f09
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
ms.openlocfilehash: db2b92e746711ced56af442e369bb40fadc4e189
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354667"
---
# <a name="difdestroyprivatedata"></a>DIF_DESTROYPRIVATEDATA


DIF_DESTROYPRIVATEDATA 请求将定向类安装程序以释放任何内存或资源分配并存储在**ClassInstallReserved**字段[ **SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)结构。

### <a name="when-sent"></a>发送时间

当 Windows 销毁[设备信息集](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)或[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)元素，或当 Windows 放弃其共同安装程序和设备类安装程序列表。

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
提供的句柄的设备信息设置。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
根据需要提供一个指向[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)标识的设备中设备的信息集的结构。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) 与关联*DeviceInfoData*、 如果指定，或与*DeviceInfoSet*.

<a href="" id="class-installation-parameters"></a>类的安装参数  
无

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters-"></a>设备安装参数   
安装程序可以清除**ClassInstallReserved**字段中的设备安装参数 ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a))。

### <a name="installer-return-value"></a>安装程序返回值

辅助安装程序不处理此 DIF 请求。 它只需在其预处理传递返回 NO_ERROR。

类安装程序通常返回 ERROR_DI_DO_DEFAULT 或 Win32 错误代码。

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

无

### <a name="installer-operation"></a>安装程序操作

类安装程序释放任何内存或资源的 DIF_DESTROYPRIVATEDATA 请求的响应中，它分配并存储在**ClassInstallReserved**字段[ **SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)结构。

不应使用共同安装程序**ClassInstallReserved**字段。

有关差异代码的详细信息，请参阅[处理 DIF 代码](https://docs.microsoft.com/windows-hardware/drivers/install/handling-dif-codes)。

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


[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






