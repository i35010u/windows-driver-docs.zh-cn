---
title: DEVPKEY_NAME（设备接口）
description: DEVPKEY_NAME（设备接口）
ms.assetid: 276862d0-8ab9-4914-9e57-834cc17d0e59
keywords:
- ) 设备和驱动程序安装 DEVPKEY_NAME (设备接口
topic_type:
- apiref
api_name:
- DEVPKEY_NAME (Device Interface)
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b3e963053ed7bc7d8e28f52b6d7641a74dcb0e9c
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716896"
---
# <a name="devpkey_name-device-interface"></a>DEVPKEY_NAME（设备接口）


DEVPKEY_NAME 设备接口属性表示设备接口的名称。

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
<td align="left"><p>安装应用程序和安装程序的只读访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_NAME 的值应用于标识用户界面项中的最终用户的接口。

如果设置了 DEVPKEY_DeviceInterface_FriendlyName，则 DEVPKEY_NAME 的值与 [**DEVPKEY_DeviceInterface_FriendlyName**](devpkey-deviceinterface-friendlyname.md) 设备属性的值相同。 否则，DEVPKEY_NAME 不存在。

可以通过调用 [**SetupDiGetDeviceInterfaceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)来检索 DEVPKEY_NAME 的值。

有关设备接口的信息，请参阅 [设备接口类](./overview-of-device-interface-classes.md) 和 [**INF AddInterface 指令**](./inf-addinterface-directive.md)。

Windows Server 2003、Windows XP 和 Windows 2000 不直接支持相应的名称属性。 但是，这些早期版本的 Windows 确实支持与 DEVPKEY_DeviceInterface_FriendlyName 相对应的属性。

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

## <a name="see-also"></a>请参阅


[**DEVPKEY_DeviceInterface_FriendlyName**](devpkey-deviceinterface-friendlyname.md)

[**INF AddInterface 指令**](./inf-addinterface-directive.md)

[**SetupDiGetDeviceInterfaceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)

 

