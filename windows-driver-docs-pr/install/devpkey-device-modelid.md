---
title: DEVPKEY_Device_ModelId
description: DEVPKEY_Device_ModelId
keywords:
- DEVPKEY_Device_ModelId 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_ModelId
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dafe2d9008e9a1bb384dbd0ca231b249682e0ef1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786795"
---
# <a name="devpkey_device_modelid"></a>DEVPKEY_Device_ModelId


DEVPKEY_Device_ModelId 设备属性将设备与 [设备元数据包](./overview-of-device-metadata-packages.md)匹配。

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
<td align="left"><p>DEVPKEY_Device_ModelId</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><a href="devprop-type-guid.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_GUID&lt;/strong&gt;](devprop-type-guid.md)"><strong>DEVPROP_TYPE_GUID</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的读取和写入访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_ModelId 设备属性为 Ihv 和 Oem 提供唯一标识共享相同制造商和型号的设备的支持。 通过使用模型标识符 (ModelID) ，Oem 和 Ihv 可以将其分发到其自己的品牌设备元数据包的设备模型相匹配。

DEVPKEY_Device_ModelId 设备属性包含设备元数据包中 [**ModelId**](/previous-versions/windows/hardware/metadata/ff549295(v=vs.85)) XML 元素的值。 安装设备后，将使用设备报告的 ModelID GUID 值填充此 PKEY。

有关详细信息，请参阅 [设备元数据包](./overview-of-device-metadata-packages.md)。

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
<td align="left"><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey (包含 Devpkey) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[设备元数据包](./overview-of-device-metadata-packages.md)

[**ModelID**](/previous-versions/windows/hardware/metadata/ff549295(v=vs.85))

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

