---
title: DEVPKEY_Device_FriendlyName
description: DEVPKEY_Device_FriendlyName
ms.assetid: 0acea25e-5068-441b-be6b-fa863d1bdba2
keywords:
- DEVPKEY_Device_FriendlyName 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_FriendlyName
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c59ef60f03ea0868eb5f01b8ba45cc3a17f4798a
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418302"
---
# <a name="devpkey_device_friendlyname"></a>DEVPKEY_Device_FriendlyName


DEVPKEY_Device_FriendlyName 设备属性表示设备实例的友好名称。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr>
<th>属性</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_FriendlyName</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的读取和写入访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_FRIENDLYNAME</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

您可以使用[**DEVPKEY_NAME**](devpkey-name--device-instance-.md)设备属性，而不是 DEVPKEY_Device_FriendlyName 在用户界面显示中显示用于标识设备实例的名称。

您可以使用 Inf DDInstall 中包含的[**AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)设置 DEVPKEY_Device_FriendlyName 的值[**。 *DDInstall***](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)安装设备的 INF 文件中的 "硬件" 部分。

可以通过调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_FriendlyName 的值，也可以通过调用[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)来设置此属性。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_FriendlyName 属性键。 相反，你可以使用相应的 SPDRP_FRIENDLYNAME 标识符来访问这些早期版本的 Windows 上的属性值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅[SPDRP_Xxx 属性访问设备实例](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**DEVPKEY_NAME（设备实例）**](devpkey-name--device-instance-.md)

[**INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)

[**INF *DDInstall*。HW 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

 






