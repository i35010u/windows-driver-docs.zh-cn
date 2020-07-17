---
title: DEVPKEY_Device_PDOName
description: DEVPKEY_Device_PDOName
ms.assetid: 1f2bc1e0-a671-47f6-9fbb-d0482b5abeca
keywords:
- DEVPKEY_Device_PDOName 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_PDOName
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 76db8c55ab1e3f5c37823f9eebb9e61c1aafeff2
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418550"
---
# <a name="devpkey_device_pdoname"></a>DEVPKEY_Device_PDOName


DEVPKEY_Device_PDOName 设备属性表示表示设备实例的物理设备对象（PDO）的名称。

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
<td align="left"><p>DEVPKEY_Device_PDOName</p></td>
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
<td align="left"><p><strong>对应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_PHYSICAL_DEVICE_OBJECT_NAME</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 将 DEVPKEY_Device_PDOName 的值设置为表示设备的物理名称对象（PDO）的名称。 有关 PDO 名称的详细信息，请参阅用于[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)例程的*DeviceName*参数。

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_PDOName 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_PDOName 属性键。 相反，你可以使用相应的 SPDRP_PHYSICAL_DEVICE_OBJECT_NAME 标识符来访问这些早期版本的 Windows 上的属性值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅[SPDRP_Xxx 属性访问设备实例](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






