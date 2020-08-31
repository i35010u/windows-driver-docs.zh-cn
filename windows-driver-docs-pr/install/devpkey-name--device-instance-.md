---
title: DEVPKEY_NAME（设备实例）
description: DEVPKEY_NAME（设备实例）
ms.assetid: 4968a215-7e22-4d17-938c-4aa5289b2803
keywords:
- ) 设备和驱动程序安装 (设备实例 DEVPKEY_NAME
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
ms.openlocfilehash: 02764d58bf55b733eafaff6dd3d18648be093b15
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095939"
---
# <a name="devpkey_name-device-instance"></a>DEVPKEY_NAME（设备实例）


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
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

应使用 DEVPKEY_NAME 设备的值来向用户界面项中的最终用户标识设备实例。

如果设置**DEVPKEY_Device_FriendlyName** ，则检索到的属性值与[**DEVPKEY_Device_FriendlyName**](devpkey-device-friendlyname.md)设备属性的值相同。 否则，DEVPKEY_NAME 的值与 [**DEVPKEY_Device_DeviceDesc**](devpkey-device-devicedesc.md) 设备属性的值相同。

可以调用 [**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_NAME 属性的值。

Windows Server 2003、Windows XP 和 Windows 2000 不直接支持相应的名称属性。 但是，这些早期版本的 Windows 确实支持与 DEVPKEY_Device_FriendlyName 和 DEVPKEY_Device_DeviceDesc 对应的属性。

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
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey (包含 Devpkey) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**DEVPKEY_Device_DeviceDesc**](devpkey-device-devicedesc.md)

[**DEVPKEY_Device_FriendlyName**](devpkey-device-friendlyname.md)

[**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

