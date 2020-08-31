---
title: DEVPKEY_Device_EjectionRelations
description: DEVPKEY_Device_EjectionRelations
ms.assetid: 3b3a0d6f-4163-40a8-817d-924f63871e51
keywords:
- DEVPKEY_Device_EjectionRelations 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_EjectionRelations
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6d2a31fc0d7f001b266ba9601cf0512d1e46418b
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095153"
---
# <a name="devpkey_device_ejectionrelations"></a>DEVPKEY_Device_EjectionRelations


DEVPKEY_Device_EjectionRelations 设备属性表示设备实例的 [**弹出关系**](../kernel/irp-mn-query-device-relations.md) 。

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
<td align="left"><p>DEVPKEY_Device_EjectionRelations</p></td>
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

可以调用 [**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_Device_EjectionRelations 的值。

Windows Server 2003、Windows XP 和 Windows 2000 不直接支持此属性。 有关如何在这些早期版本的 Windows 上检索设备关系属性的信息，请参阅 [检索设备关系](./retrieving-device-relations.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>另请参阅


[**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

