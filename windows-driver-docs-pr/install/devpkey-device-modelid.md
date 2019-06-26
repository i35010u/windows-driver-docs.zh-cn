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
ms.openlocfilehash: a9de4d826e790ddfe3ebbb4e5c596250fc0e8b5e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378177"
---
# <a name="devpkeydevicemodelid"></a>DEVPKEY_Device_ModelId


DEVPKEY_Device_ModelId 设备属性与匹配的设备[设备元数据包](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
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
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>读取和写入访问权限通过安装应用程序和安装程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_ModelId 设备属性提供对来唯一地标识共享相同的制造商和型号的设备的 Ihv 和 Oem 的支持。 通过使用模型标识符 (ModelID)，Oem 和 Ihv 可以匹配它们分发给其自己的经过品牌打造的设备元数据包的设备模型。

DEVPKEY_Device_ModelId 设备属性包含的值[ **ModelID** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549295(v=vs.85))从设备元数据包的 XML 元素。 安装设备时，报告的设备使用 ModelID GUID 值填充此主键。

有关详细信息，请参阅[设备元数据包](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)。

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
<td align="left"><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[设备元数据包](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)

[**ModelID**](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549295(v=vs.85))

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






