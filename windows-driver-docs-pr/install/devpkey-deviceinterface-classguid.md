---
title: DEVPKEY_DeviceInterface_ClassGuid
description: DEVPKEY_DeviceInterface_ClassGuid
ms.assetid: f7346189-9986-4b26-b059-b1a58c8313d1
keywords:
- DEVPKEY_DeviceInterface_ClassGuid 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceInterface_ClassGuid
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 37f96eae11e30546985067be05a3f9f9bf522396
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716382"
---
# <a name="devpkey_deviceinterface_classguid"></a>DEVPKEY_DeviceInterface_ClassGuid


DEVPKEY_DeviceInterface_ClassGuid 设备属性表示标识设备接口类的 GUID。

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
<td align="left"><p>DEVPKEY_DeviceInterface_ClassGuid</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-guid.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_GUID&lt;/strong&gt;](devprop-type-guid.md)"><strong>DEVPROP_TYPE_GUID</strong></a></p></td>
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

{*设备接口类*} 密钥值的格式为 "{*nnnnnnnn* - *nnnn* - *nnnn* - *nnnn* - *nnnnnnnnnnnn*}"，其中每个*n*是一个十六进制数字。

可以调用 [**SetupDiGetDeviceInterfaceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw) 来检索 DEVPKEY_DeviceInterface_ClassGuid 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_DeviceInterface_ClassGuid 属性键。 有关如何在这些早期版本的 Windows 上检索设备接口的类 GUID 的信息，请参阅有关如何使用在[访问设备接口属性](./accessing-device-interface-properties.md)中提供的[**SetupDiEnumDeviceInterfaces**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)的信息。

有关如何安装和访问设备接口的信息，请参阅 [设备接口类](./overview-of-device-interface-classes.md) 和 [**INF AddInterface 指令**](./inf-addinterface-directive.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**INF AddInterface 指令**](./inf-addinterface-directive.md)

[**SetupDiEnumDeviceInterfaces**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)

[**SetupDiGetDeviceInterfaceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)

 

