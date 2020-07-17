---
title: DEVPKEY_Device_LocationInfo
description: DEVPKEY_Device_LocationInfo
ms.assetid: c7eba222-20fe-4868-89e2-9dcef9965cec
keywords:
- DEVPKEY_Device_LocationInfo 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_LocationInfo
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b2fd1f26a2c707a4a4b967f8ff7da0105cd89a14
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418555"
---
# <a name="devpkey_device_locationinfo"></a>DEVPKEY_Device_LocationInfo


DEVPKEY_Device_LocationInfo 设备属性表示设备实例的特定于总线的物理位置。

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
<td align="left"><p>DEVPKEY_Device_LocationInfo</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的读取和写入访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_LOCATION_INFORMATION</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 将 DEVPKEY_Device_LocationInfo 的值设置为用于响应[**IRP_MN_QUERY_DEVICE_TEXT**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text) IRP 的设备实例的值。

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)和**SetupDiGetDeviceProperty**检索和设置 DEVPKEY_Device_LocationInfo 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_LocationInfo 属性键。 相反，你可以使用相应的 SPDRP_LOCATION_INFORMATION 标识符来访问这些早期版本的 Windows 上的属性值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅[SPDRP_Xxx 属性访问设备实例](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**IRP_MN_QUERY_DEVICE_TEXT**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-text)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






