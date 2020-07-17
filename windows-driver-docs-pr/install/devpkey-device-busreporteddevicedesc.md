---
title: DEVPKEY_Device_BusReportedDeviceDesc
description: DEVPKEY_Device_BusReportedDeviceDesc
ms.assetid: 3a03b4f0-728c-4a15-9c97-03d03f65afc7
keywords:
- DEVPKEY_Device_BusReportedDeviceDesc 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_BusReportedDeviceDesc
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bf2af5c130fbd34266662c1c9f2387971434e214
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418514"
---
# <a name="devpkey_device_busreporteddevicedesc"></a>DEVPKEY_Device_BusReportedDeviceDesc


DEVPKEY_Device_BusReportedDeviceDesc 设备属性表示设备实例的总线驱动程序报告的字符串值。

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
<td align="left"><p>DEVPKEY_Device_BusReportedDeviceDesc</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_BusReportedDeviceDesc 的值由 Windows 即插即用（PnP）设置，其字符串值为设备实例的总线驱动程序报告的字符串值。 在用[**IRP_MN_QUERY_DEVICE_TEXT**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)进行查询时，总线驱动程序会返回此值。

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_BusReportedDeviceDesc 的值。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey （包括 Devpkey）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






