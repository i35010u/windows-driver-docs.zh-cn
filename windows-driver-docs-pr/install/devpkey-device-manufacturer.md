---
title: DEVPKEY_Device_Manufacturer
description: DEVPKEY_Device_Manufacturer
ms.assetid: 28da7262-bdb6-40da-a2f8-30dcbd4f5e6c
keywords:
- DEVPKEY_Device_Manufacturer 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Manufacturer
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0b74b928028a5ad0cf21194963dd4a128dfc3db5
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096819"
---
# <a name="devpkey_device_manufacturer"></a>DEVPKEY_Device_Manufacturer


DEVPKEY_DEVICE_Manufacturer 设备属性表示设备实例的制造商的名称。

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
<td align="left"><p>DEVPKEY_Device_Manufacturer</p></td>
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
<td align="left"><p><strong>对应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_MFG</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_DEVICE_Manufacturer 的值由安装设备的 INF 文件的 " [**Inf 制造商" 部分**](./inf-manufacturer-section.md)提供的设备的*制造商标识符*输入值设置。

可以调用 [**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_DEVICE_Manufacturer 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_Manufacturer 属性键。 相反，你可以使用相应的 SPDRP_MFG 标识符来访问这些早期版本的 Windows 上的属性值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅 [SPDRP_Xxx 属性访问设备实例](./accessing-device-instance-spdrp-xxx-properties.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>另请参阅


[**INF Manufacturer 节**](./inf-manufacturer-section.md)

[**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

