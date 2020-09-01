---
title: DEVPKEY_Device_FirstInstallDate
description: DEVPKEY_Device_FirstInstallDate
ms.assetid: aedc4f18-51be-4c42-a172-c1fd88cc49b3
keywords:
- DEVPKEY_Device_FirstInstallDate 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_FirstInstallDate
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4c1cd36e87a9a51e6ed1f431d3efe79153e51e12
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096841"
---
# <a name="devpkey_device_firstinstalldate"></a>DEVPKEY_Device_FirstInstallDate


DEVPKEY_Device_FirstInstallDate 设备属性指定设备实例首次安装到系统中时的时间戳。

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
<td align="left"><p>DEVPKEY_Device_FirstInstallDate</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-filetime.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_FILETIME&lt;/strong&gt;](devprop-type-filetime.md)"><strong>DEVPROP_TYPE_FILETIME</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 将 DEVPKEY_Device_FirstInstallDate 的值设置为时间戳，该时间戳指定第一次在系统中安装设备实例的时间。

**注意**   与[**DEVPKEY_Device_InstallDate**](devpkey-device-installdate.md)属性不同，每次更新设备驱动程序时，DEVPKEY_Device_FirstInstallDate 属性的值不会更改。 例如，通过 Windows 更新更新的驱动程序不会更改此属性的值。

 

可以调用 [**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_Device_FirstInstallDate 属性的值。

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


[**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

