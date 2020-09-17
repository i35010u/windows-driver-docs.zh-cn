---
title: DEVPKEY_Device_Legacy
description: DEVPKEY_Device_Legacy
ms.assetid: a2af9881-3aa3-45a7-9b80-cb507460957e
keywords:
- DEVPKEY_Device_Legacy 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Legacy
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b40663b325a7fe256a3229240cefa14854f59101
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714664"
---
# <a name="devpkey_device_legacy"></a>DEVPKEY_Device_Legacy


DEVPKEY_Device_Legacy 设备属性表示一个布尔值，该值指示设备是否为根枚举设备，该设备在加载设备的非 PnP 驱动程序时自动创建即插即用 (PnP) 管理器。

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
<td align="left"><p>DEVPKEY_Device_Legacy</p></td>
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

PnP 管理器将 DEVPKEY_Device_Reported 的值设置为 DEVPROP_TRUE 如果在加载设备的非 PnP 驱动程序时，PnP 管理器自动将设备创建为根枚举设备。 否则，PnP 管理器会将属性的值设置为 DEVPROP_FALSE。

可以调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_Device_Legacy 的值。

Windows Server 2003、Windows XP 和 Windows 2000 不支持此属性。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

