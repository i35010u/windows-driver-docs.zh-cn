---
title: DEVPKEY_Device_PowerRelations
description: DEVPKEY_Device_PowerRelations
ms.assetid: 616e6d02-9047-491b-b7e7-758e1804dff5
keywords:
- DEVPKEY_Device_PowerRelations 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_PowerRelations
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7de658f66d005123dcd2179762100a7c5fd5b543
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327223"
---
# <a name="devpkeydevicepowerrelations"></a>DEVPKEY_Device_PowerRelations


DEVPKEY_Device_PowerRelations 设备属性表示[**电源关系**](https://msdn.microsoft.com/library/windows/hardware/ff551670)设备实例。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_PowerRelations</p></td>
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

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)检索 DEVPKEY_Device_PowerRelations 值。

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


[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






