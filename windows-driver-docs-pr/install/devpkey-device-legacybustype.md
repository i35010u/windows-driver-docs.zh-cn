---
title: DEVPKEY_Device_LegacyBusType
description: DEVPKEY_Device_LegacyBusType
ms.assetid: 76c2a472-bb05-4f6a-84da-0ae9e7c1fdf1
keywords:
- DEVPKEY_Device_LegacyBusType 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_LegacyBusType
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 17094a44209f6d4350226790d5268057210075c0
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714660"
---
# <a name="devpkey_device_legacybustype"></a>DEVPKEY_Device_LegacyBusType


DEVPKEY_Device_LegacyBusType 设备属性表示设备实例的旧总线号。

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
<td align="left"><p>DEVPKEY_Device_LegacyBusType</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_LEGACYBUSTYPE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 将 DEVPKEY_Device_LegacyBusType 的值设置为总线驱动程序为响应[**IRP_MN_QUERY_BUS_INFORMATION**](../kernel/irp-mn-query-bus-information.md)请求而返回的[**PNP_BUS_INFORMATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_pnp_bus_information)结构的 LegacyBusType 成员的值。 DEVPKEY_Device_LegacyBusType 的值是在 Ntddk 和中定义的 [**INTERFACE_TYPE**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_interface_type) 枚举器值之一。

可以调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_Device_LegacyBusType 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_LegacyBusType 属性键。 相反，你可以使用相应的 SPDRP_LEGACYBUSTYPE 标识符来访问这些早期版本的 Windows 上的属性值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅 [SPDRP_Xxx 属性访问设备实例](./accessing-device-instance-spdrp-xxx-properties.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**INTERFACE_TYPE**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_interface_type)

[**IRP_MN_QUERY_BUS_INFORMATION**](../kernel/irp-mn-query-bus-information.md)

[**PNP_BUS_INFORMATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_pnp_bus_information)

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

