---
title: DEVPKEY_DeviceClass_DevType
description: DEVPKEY_DeviceClass_DevType
ms.assetid: 383f2b47-c0ee-49c2-851c-b18c98fd0303
keywords:
- DEVPKEY_DeviceClass_DevType 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_DevType
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dfaa666e4201e23630f2eba05bb63294c5bceac4
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714616"
---
# <a name="devpkey_deviceclass_devtype"></a>DEVPKEY_DeviceClass_DevType


DEVPKEY_DeviceClass_DevType 设备属性表示 [设备安装程序类](./overview-of-device-setup-classes.md)的默认设备类型。

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
<td align="left"><p>DEVPKEY_DeviceClass_DevType</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-uint32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_UINT32&lt;/strong&gt;](devprop-type-uint32.md)"><strong>DEVPROP_TYPE_UINT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序后，安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应 SPCRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPCRP_DEVTYPE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

安装应用程序安装设备安装程序类时，可以设置 DEVPKEY_DeviceClass_DevType 的值。 有关如何安装设备安装程序类和设置此属性的信息，请参阅[**Inf ClassInstall32 部分**](./inf-classinstall32-section.md)和有关注册表项值**DeviceType**的信息，请参阅[**Inf AddReg 指令**](./inf-addreg-directive.md)的 "特殊的*值-名称*关键字" 部分。

DEVPKEY_DeviceClass_DevType 的值是在 Ntddk 和中定义的 FILE_DEVICE_Xxx 值之一。 有关设备类型的详细信息，请参阅[**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)函数的*DeviceType*参数。

可以调用 [**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw) 或 [**SetupDiGetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyexw) 来检索 DEVPKEY_DeviceClass_DevType 的值。

Windows Server 2003 和 Windows XP 支持此属性，但不支持 DEVPKEY_DeviceClass_DevType 属性键。 在这些早期版本的 Windows 中，可以使用 SPCRP_DEVTYPE 标识符来访问此属性的值。 有关如何访问此属性的值的信息，请参阅 [检索设备安装程序类 SPCRP_Xxx 属性](./retrieving-spcrp-xxx-properties.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)

[**INF AddReg 指令**](./inf-addreg-directive.md)

[**INF ClassInstall32 节**](./inf-classinstall32-section.md)

[**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

 

