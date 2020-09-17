---
title: DEVPKEY_Device_InstanceId
description: DEVPKEY_Device_InstanceId
ms.assetid: 74c78289-e140-46da-8005-ef6f441f78ec
keywords:
- DEVPKEY_Device_InstanceId 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_InstanceId
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ee629d644503420d1b31637077cf08a574500e62
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714666"
---
# <a name="devpkey_device_instanceid"></a>DEVPKEY_Device_InstanceId


DEVPKEY_Device_InstanceId 设备属性表示设备的设备实例标识符。

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
<td align="left"><p>DEVPKEY_Device_InstanceId</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
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

DEVPKEY_Device_InstanceId 的值由 Windows 在设备实例的安装过程中进行设置。

可以调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索设备实例的 DEVPKEY_Device_InstanceId 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_InstanceId 属性键。 有关如何在这些早期版本的 Windows 上检索设备实例标识符的信息，请参阅 [检索设备实例标识符](./retrieving-a-device-instance-identifier.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceInstanceId**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinstanceida)

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

