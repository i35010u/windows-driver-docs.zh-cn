---
title: DEVPKEY_Device_RemovalRelations
description: DEVPKEY_Device_RemovalRelations
ms.assetid: c88e2545-0c7b-4f8f-93f2-b9de1ec0444c
keywords:
- DEVPKEY_Device_RemovalRelations 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_RemovalRelations
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8a5c3b64a0b301b78dbee8025c91a0da8afd0b95
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522181"
---
# <a name="devpkeydeviceremovalrelations"></a>DEVPKEY_Device_RemovalRelations


DEVPKEY_Device_RemovalRelations 设备属性表示[**删除关系**](https://msdn.microsoft.com/library/windows/hardware/ff551670)设备实例。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_RemovalRelations</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>不适用</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)检索 DEVPKEY_Device_RemovalRelations 值。

Windows Server 2003、 Windows XP 和 Windows 2000 不直接支持此属性。 有关如何检索这些早期版本的 Windows 上的设备的关系属性的信息，请参阅[检索设备关系](https://msdn.microsoft.com/library/windows/hardware/ff550630)。

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


[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






