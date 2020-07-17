---
title: DEVPKEY_Device_Reported
description: DEVPKEY_Device_Reported
ms.assetid: dfec9e24-4d4e-42e4-a229-ad3d060fb1b5
keywords:
- DEVPKEY_Device_Reported 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_Reported
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a69e14017082dade0e7773461e86d178190a69c3
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418433"
---
# <a name="devpkey_device_reported"></a>DEVPKEY_Device_Reported


DEVPKEY_Device_Reported 设备属性表示一个布尔值，该值指示设备实例是否为根枚举设备，设备的驱动程序通过调用[**IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)向即插即用（PnP）管理器报告该设备。

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
<td align="left"><p>DEVPKEY_Device_Reported</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
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

PnP 管理器将 DEVPKEY_Device_Reported 的值设置为 DEVPROP_TRUE 如果设备是一个根枚举设备，则设备的驱动程序会通过调用 IoReportDetectedDevice 向 PnP 管理器报告该设备。 否则，PnP 管理器会将属性的值设置为 DEVPROP_FALSE。

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_Reported 的值。

Windows Server 2003、Windows XP 和 Windows 2000 不支持此属性。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






