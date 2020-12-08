---
title: DEVPKEY_Device_Children
description: DEVPKEY_Device_Children
keywords:
- DEVPKEY_Device_Children 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Children
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: de7804fedb7d82efabd85df3adf3167a6165f0cd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840087"
---
# <a name="devpkey_device_children"></a>DEVPKEY_Device_Children


DEVPKEY_Device_Children 设备属性表示作为设备实例子级的设备的设备实例 Id 列表。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr>
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_Children</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>不适用</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_Device_Children 的值。

Windows Server 2003、Windows XP 和 Windows 2000 不直接支持此属性。 有关如何在这些早期版本的 Windows 上检索设备关系属性的信息，请参阅 [检索设备关系](./retrieving-device-relations.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

