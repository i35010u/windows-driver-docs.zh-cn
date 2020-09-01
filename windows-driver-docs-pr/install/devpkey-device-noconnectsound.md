---
title: DEVPKEY_Device_NoConnectSound
description: DEVPKEY_Device_NoConnectSound
ms.assetid: 7ed4eb3f-6585-4ec1-83b7-bde368faca0a
keywords:
- DEVPKEY_Device_NoConnectSound 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_NoConnectSound
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 573d0569643ec217a95acf698aba8a0991cf364d
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096807"
---
# <a name="devpkey_device_noconnectsound"></a>DEVPKEY_Device_NoConnectSound


DEVPKEY_Device_NoConnectSound 设备属性表示一个布尔值，该值指示是否禁止 Microsoft Windows 操作系统播放的声音指示可移动设备已到达或已被删除。

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
<td align="left"><p>DEVPKEY_Device_NoConnectSound</p></td>
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
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_NoConnectSound 的值设置为 DEVPROP_TRUE 以取消播放声音。 否则，属性的值将设置为 DEVPROP_FALSE。

DEVPKEY_Device_NoConnectSound 属性通常由设备 INF 文件中的 [**Inf AddProperty 指令**](./inf-addproperty-directive.md) 设置。

可以调用 [**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 或 [**SetupDiSetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw) 来检索或设置 DEVPKEY_Device_NoConnectSound 的值。

Windows Server 2003、Windows XP 和 Windows 2000 不支持此属性。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>另请参阅


[**INF AddProperty 指令**](./inf-addproperty-directive.md)

[**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

