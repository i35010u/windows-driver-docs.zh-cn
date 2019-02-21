---
title: DEVPKEY_Device_PhysicalDeviceLocation
description: DEVPKEY_Device_PhysicalDeviceLocation
ms.assetid: DEF01D17-7E32-45BB-8846-D3B3B60506EB
keywords:
- DEVPKEY_Device_PhysicalDeviceLocation 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_PhysicalDeviceLocation
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 580beb199fac00a965011bc3e28d23ceeacd2a8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522671"
---
# <a name="devpkeydevicephysicaldevicelocation"></a>DEVPKEY_Device_PhysicalDeviceLocation


DEVPKEY_Device_PhysicalDeviceLocation 设备属性封装到 Windows 提供的设备的固件的物理设备位置信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_PhysicalDeviceLocation</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BINARY&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_BINARY</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>相应 SPDRP_<em>Xxx</em></strong>  <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_PHYSICAL_DEVICE_LOCATION</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 设置的值 DEVPKEY_Device_PhysicalDeviceLocation 与物理设备的位置信息。 ACPI 4.0 a 中定义的信息的格式规范中，部分 6.1.6。

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)检索 DEVPKEY_Device_PhysicalDeviceLocation 值。

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
<td align="left"><p>可从 Windows 8 开始</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






