---
title: DEVPKEY_Device_BusRelations
description: DEVPKEY_Device_BusRelations
ms.assetid: 590cbf77-3cee-4c74-bad1-ca237986cff0
keywords:
- DEVPKEY_Device_BusRelations 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_BusRelations
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 13948399d7aa186e21c7a37335cc5a095ef674c4
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418546"
---
# <a name="devpkey_device_busrelations"></a>DEVPKEY_Device_BusRelations


DEVPKEY_Device_BusRelations 设备属性表示设备实例的[**总线关系**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)。

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
<td align="left"><p>DEVPKEY_Device_BusRelations</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>不适用</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_BusRelations 的值。

Windows Server 2003、Windows XP 和 Windows 2000 不直接支持此属性。 有关如何在这些早期版本的 Windows 上检索设备关系属性的信息，请参阅[检索设备关系](https://docs.microsoft.com/windows-hardware/drivers/install/retrieving-device-relations)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






