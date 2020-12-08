---
title: DEVPKEY_DeviceInterface_Enabled
description: DEVPKEY_DeviceInterface_Enabled
keywords:
- DEVPKEY_DeviceInterface_Enabled 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceInterface_Enabled
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3c91c81e5333ed38539597d1513406efcc6c26aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841245"
---
# <a name="devpkey_deviceinterface_enabled"></a>DEVPKEY_DeviceInterface_Enabled


**DeviceInterfaceEnabled** 设备属性表示一个布尔型标志，该标志指示是否已启用设备接口。

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
<td align="left"><p>DEVPKEY_DeviceInterface_Enabled</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>由安装应用程序和安装程序只读</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果 DEVPROP_TRUE DEVPKEY_DeviceInterface_Enabled 的值，则会启用接口。 否则，接口将不启用。

可以调用 [**SetupDiGetDeviceInterfaceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw) 来检索 DEVPKEY_DeviceInterface_Enabled 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_DeviceInterface_Enabled 属性键。 有关如何在这些早期版本的 Windows 上检索设备接口的活动状态的信息，请参阅有关如何使用在 [访问设备接口属性](./accessing-device-interface-properties.md)中提供的 [**SetupDiEnumDeviceInterfaces**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)的信息。

有关设备接口的详细信息，请参阅 [设备接口类](./overview-of-device-interface-classes.md) 和 [**INF AddInterface 指令**](./inf-addinterface-directive.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**INF AddInterface 指令**](./inf-addinterface-directive.md)

[**SetupDiEnumDeviceInterfaces**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)

[**SetupDiGetDeviceInterfaceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)

 

