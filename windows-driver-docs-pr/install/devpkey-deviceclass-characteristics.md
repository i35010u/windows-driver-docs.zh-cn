---
title: DEVPKEY_DeviceClass_Characteristics
description: DEVPKEY_DeviceClass_Characteristics
ms.assetid: dd50a97b-7230-46a5-b6d2-0f741d7ae5d4
keywords:
- DEVPKEY_DeviceClass_Characteristics 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_Characteristics
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 33498f42d3f85283d17cc1a6ded2c57abdb183cd
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715588"
---
# <a name="devpkey_deviceclass_characteristics"></a>DEVPKEY_DeviceClass_Characteristics


DEVPKEY_DeviceClass_Characteristics 设备属性表示 [设备安装程序类](./overview-of-device-setup-classes.md)中所有设备的默认设备特征。

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
<td align="left"><p>DEVPKEY_DeviceClass_Characteristics</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序后，安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应 SPCRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPCRP_CHARACTERISTICS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

仅当安装了设备安装程序类而不是稍后进行修改时，才应设置 DEVPKEY_DeviceClass_Characteristics。 有关如何安装设备安装程序类和设置此属性的信息，请参阅[**Inf ClassInstall32 部分**](./inf-classinstall32-section.md)和有关注册表项值**DeviceCharacteristics**的信息，请参阅[**Inf AddReg 指令**](./inf-addreg-directive.md)的 "特殊的*值-名称*关键字" 部分。

可以调用 [**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw) 或 [**SetupDiGetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyexw) 来检索 DEVPKEY_DeviceClass_Characteristics 的值。

Windows Server 2003 和 Windows XP 支持此属性，但不支持 DEVPKEY_DeviceClass_Characteristics 属性键。 在这些早期版本的 Windows 中，可以使用 SPCRP_CHARACTERISTICS 标识符来访问此属性的值。 有关如何访问此属性的值的信息，请参阅 [检索设备安装程序类 SPCRP_Xxx 属性](./retrieving-spcrp-xxx-properties.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)

[**INF AddReg 指令**](./inf-addreg-directive.md)

[**INF ClassInstall32 节**](./inf-classinstall32-section.md)

[**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

 

