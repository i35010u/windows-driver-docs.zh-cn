---
title: DEVPKEY_Device_ModelId
description: DEVPKEY_Device_ModelId
ms.assetid: 6066f18b-40bf-4b36-9821-5e886e166256
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
ms.openlocfilehash: 335a46c332e2e44e089eeda90423db5a9378f521
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096809"
---
# <a name="devpkey_device_modelid"></a>DEVPKEY_Device_ModelId


DEVPKEY_Device_ModelId 设备属性将设备与 [设备元数据包](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)匹配。

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

有关详细信息，请参阅 [设备元数据包](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)。

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

## <a name="see-also"></a>另请参阅


[设备元数据包](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)

[**ModelID**](/previous-versions/windows/hardware/metadata/ff549295(v=vs.85))

[**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

