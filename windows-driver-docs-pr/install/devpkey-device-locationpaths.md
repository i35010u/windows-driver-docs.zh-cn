---
title: DEVPKEY_Device_LocationPaths
description: DEVPKEY_Device_LocationPaths
ms.assetid: 36320528-d306-441f-a7ae-5a75d982b32a
keywords:
- DEVPKEY_Device_LocationPaths 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_LocationPaths
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d2387afcb2037372b9cd6d8257d593996001cc08
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418560"
---
# <a name="devpkey_device_locationpaths"></a>DEVPKEY_Device_LocationPaths


DEVPKEY_Device_LocationPaths 设备属性表示设备树中设备实例的位置。

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
<td align="left"><p>DEVPKEY_Device_LocationPaths</p></td>
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
<td align="left"><p><strong>对应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_LOCATION_PATHS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 设置 DEVPKEY_Device_LocationPaths 的值。

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_LocationPaths 的值。

Windows Server 2003 支持此属性，但不支持 DEVPKEY_Device_LocationPaths 属性键。 相反，你可以使用相应的 SPDRP_LOCATION_PATHS 标识符来访问 Windows Server 2003 上的属性的值。 有关如何在 Windows Server 2003 上访问此属性值的信息，请参阅[SPDRP_Xxx 属性访问设备实例](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






