---
title: DEVPKEY_Device_Exclusive
description: DEVPKEY_Device_Exclusive
ms.assetid: c54c2fe3-cf57-4603-a701-8ddbc28aa47d
keywords:
- DEVPKEY_Device_Exclusive 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Exclusive
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 073d3bb76c474e87a735b6d42782c27fe4d25585
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096837"
---
# <a name="devpkey_device_exclusive"></a>DEVPKEY_Device_Exclusive


DEVPKEY_Device_Exclusive 设备属性表示一个布尔值，该值确定是否可以打开设备实例以供独占使用。

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
<td align="left"><p>DEVPKEY_Device_Exclusive</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的读取和写入访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_EXCLUSIVE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果可以打开设备以供独占使用，则 DEVPROP_TRUE DEVPKEY_Device_Exclusive 属性的值。 否则，属性的值为 DEVPROP_FALSE。

您可以使用 Inf DDInstall 中包含的[**AddReg 指令**](./inf-addreg-directive.md)设置 DEVPKEY_Device_Exclusive 的值[**。 *DDInstall***](./inf-ddinstall-hw-section.md)安装设备的硬件部分。

可以通过调用 [**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 和 [**SetupDiSetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)检索或设置 DEVPKEY_Device_Exclusive 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_Exclusive 属性键。 相反，你可以使用相应的 SPDRP_EXCLUSIVE 标识符来访问这些早期版本的 Windows 上的属性值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅 [SPDRP_Xxx 属性访问设备实例](./accessing-device-instance-spdrp-xxx-properties.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>另请参阅


[**INF AddReg 指令**](./inf-addreg-directive.md)

[**INF *DDInstall*。HW 部分**](./inf-ddinstall-hw-section.md)

[**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

