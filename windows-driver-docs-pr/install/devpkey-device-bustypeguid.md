---
title: DEVPKEY_Device_BusTypeGuid
description: DEVPKEY_Device_BusTypeGuid
ms.assetid: a68e7ff2-9afa-48d5-9764-3c400561024e
keywords:
- DEVPKEY_Device_BusTypeGuid 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_BusTypeGuid
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 59eaed3eb2f2674ffb0fd7b88435e1b3d72077a8
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418515"
---
# <a name="devpkey_device_bustypeguid"></a>DEVPKEY_Device_BusTypeGuid


DEVPKEY_Device_BusTypeGuid 设备属性表示标识设备实例的总线类型的 GUID。

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
<td align="left"><p>DEVPKEY_Device_BusTypeGuid</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-guid.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_GUID&lt;/strong&gt;](devprop-type-guid.md)"><strong>DEVPROP_TYPE_GUID</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_BUSTYPEGUID</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 将 DEVPKEY_Device_BusTypeGuid 的值设置为总线驱动程序为响应[**IRP_MN_QUERY_BUS_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-bus-information)请求而返回的[**PNP_BUS_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pnp_bus_information)结构的 BusTypeGuid 成员的值。

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_BusTypeGuid 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_BusTypeGuid 属性键。 相反，你可以使用相应的 SPDRP_BUSTYPEGUID 标识符来访问这些早期版本的 Windows 上的属性值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅[SPDRP_Xxx 属性访问设备实例](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**IRP_MN_QUERY_BUS_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-bus-information)

[**PNP_BUS_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_pnp_bus_information)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






