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
ms.openlocfilehash: b2eb5d11203fb0b6f43c95a4295311ea45606dcc
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418216"
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
<th>属性</th>
<th>Value</th>
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

可以调用[**SetupDiGetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)来检索 DEVPKEY_DeviceInterface_ClassGuid 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_DeviceInterface_ClassGuid 属性键。 有关如何在这些早期版本的 Windows 上检索设备接口的类 GUID 的信息，请参阅有关如何使用在[访问设备接口属性](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-interface-properties)中提供的[**SetupDiEnumDeviceInterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)的信息。

有关如何安装和访问设备接口的信息，请参阅[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)和[**INF AddInterface 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**INF AddInterface 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)

[**SetupDiEnumDeviceInterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)

[**SetupDiGetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)

 

 






