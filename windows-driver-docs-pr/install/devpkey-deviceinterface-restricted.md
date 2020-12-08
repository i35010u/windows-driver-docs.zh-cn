---
title: DEVPKEY_DeviceInterface_Restricted
description: DEVPKEY_DeviceInterface_Restricted
keywords:
- DEVPKEY_DeviceInterface_Restricted 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceInterface_Restricted
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6c434f402d489c0a7cbce9e7e788265867f20210
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840069"
---
# <a name="devpkey_deviceinterface_restricted"></a>DEVPKEY_DeviceInterface_Restricted


DEVPKEY_DeviceInterface_Restricted 设备接口属性指示其所在的设备接口并设置为 TRUE，应由遵循该设置的系统组件的特权访问进行处理。

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
<td align="left"><p>DEVPKEY_DeviceInterface_Restricted</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以调用 [**SetupDiGetDeviceInterfaceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw) 来检索 DEVPKEY_DeviceInterface_Restricted 的值。

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
<td align="left"><p>从 Windows 8 开始可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey (包含 Devpkey) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceInterfaceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)

 

