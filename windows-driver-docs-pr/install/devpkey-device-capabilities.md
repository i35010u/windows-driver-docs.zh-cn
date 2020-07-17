---
title: DEVPKEY_Device_Capabilities
description: DEVPKEY_Device_Capabilities
ms.assetid: 8bda0c77-b711-41a9-9feb-52b22de224f0
keywords:
- DEVPKEY_Device_Capabilities 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Capabilities
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c5d5d417446c04a33438260f06f06f8b79fd9614
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418510"
---
# <a name="devpkey_device_capabilities"></a>DEVPKEY_Device_Capabilities


DEVPKEY_Device_Capabilities 设备属性表示设备实例的功能。

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
<td align="left"><p>DEVPKEY_Device_Capabilities</p></td>
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
<td align="left"><p>SPDRP_CAPABILITIES</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 将 DEVPKEY_Device_Capabilities 的值设置为响应设备功能信息的[**IRP_MN_QUERY_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)请求而返回的功能值。 DEVPKEY_Device_Capabilities 的值是在 Cfgmgr32 中定义的 CM_DEVCAP_*Xxx*功能标志的按位 "或"。 这些标志所表示的设备功能对应于[**DEVICE_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构的成员的一个子集。

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_Capabilities 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_Capabilities 属性键。 相反，你可以使用相应的 SPDRP_CAPABILITIES 标识符来访问这些早期版本的 Windows 上的属性值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅[SPDRP_Xxx 属性访问设备实例](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**DEVICE_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)

[**IRP_MN_QUERY_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






