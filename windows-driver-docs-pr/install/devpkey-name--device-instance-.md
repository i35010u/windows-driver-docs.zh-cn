---
title: DEVPKEY_NAME（设备实例）
description: DEVPKEY_NAME（设备实例）
ms.assetid: 4968a215-7e22-4d17-938c-4aa5289b2803
keywords:
- DEVPKEY_NAME （设备实例） 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_NAME (Device Instance)
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e7c9e7875f65acf4fc691b2d7b111b18a83664e8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377259"
---
# <a name="devpkeyname-device-instance"></a>DEVPKEY_NAME（设备实例）


DEVPKEY_NAME 设备属性表示设备实例的名称。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_NAME</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_NAME 设备的值应该用于标识向用户界面项目中的最终用户的设备实例。

检索到的属性值是相同的值[ **DEVPKEY_Device_FriendlyName** ](devpkey-device-friendlyname.md)设备属性，如果**DEVPKEY_Device_FriendlyName**设置。 否则，DEVPKEY_NAME 的值是相同的值[ **DEVPKEY_Device_DeviceDesc** ](devpkey-device-devicedesc.md)设备属性。

您可以调用[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)检索 DEVPKEY_NAME 属性的值。

Windows Server 2003、 Windows XP 和 Windows 2000 不直接支持相应的 name 属性。 但是，这些早期版本的 Windows 支持与 DEVPKEY_Device_FriendlyName 和 DEVPKEY_Device_DeviceDesc 相对应的属性。

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
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DEVPKEY_Device_DeviceDesc**](devpkey-device-devicedesc.md)

[**DEVPKEY_Device_FriendlyName**](devpkey-device-friendlyname.md)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






