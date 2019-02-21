---
title: DEVPKEY_NAME （设备接口）
description: DEVPKEY_NAME （设备接口）
ms.assetid: 276862d0-8ab9-4914-9e57-834cc17d0e59
keywords:
- DEVPKEY_NAME （设备接口） 设备和驱动程序安装
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
ms.openlocfilehash: 96d917d97f39fefc1117d19228251d0f792e4314
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522868"
---
# <a name="devpkeyname-device-interface"></a>DEVPKEY_NAME （设备接口）


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
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_NAME 的值应该用于标识用户界面项目中的最终用户的接口。

DEVPKEY_NAME 的值是相同的值[ **DEVPKEY_DeviceInterface_FriendlyName** ](devpkey-deviceinterface-friendlyname.md)设备属性，如果 DEVPKEY_DeviceInterface_FriendlyName 设置。 否则，DEVPKEY_NAME 不存在。

可以通过调用检索的值 DEVPKEY_NAME [ **SetupDiGetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551122)。

有关设备接口的信息，请参阅[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)并[ **INF AddInterface 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546310)。

Windows Server 2003、 Windows XP 和 Windows 2000 不直接支持相应的 name 属性。 但是，这些早期版本的 Windows 支持到 DEVPKEY_DeviceInterface_FriendlyName 相对应的属性。

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
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**DEVPKEY_DeviceInterface_FriendlyName**](devpkey-deviceinterface-friendlyname.md)

[**INF AddInterface Directive**](https://msdn.microsoft.com/library/windows/hardware/ff546310)

[**SetupDiGetDeviceInterfaceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551122)

 

 






