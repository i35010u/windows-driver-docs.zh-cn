---
title: DEVPKEY_Device_LowerFilters
description: DEVPKEY_Device_LowerFilters
ms.assetid: 7ee0421f-7c4e-463a-ab79-1616c6837bdc
keywords:
- DEVPKEY_Device_LowerFilters 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_LowerFilters
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e5a8ca50f934ab97da998e998be9768e60043be4
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714662"
---
# <a name="devpkey_device_lowerfilters"></a>DEVPKEY_Device_LowerFilters


DEVPKEY_Device_LowerFilters 设备属性表示为设备实例安装的低级筛选器驱动程序的服务名称列表。

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
<td align="left"><p>DEVPKEY_Device_LowerFilters</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的读取和写入访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_LOWERFILTERS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

为设备安装较低级别的设备筛选器驱动程序时，将设置 DEVPKEY_Device_LowerFilters 属性的值。 有关如何安装设备筛选器驱动程序的详细信息，请参阅 [安装筛选器驱动程序](./installing-a-filter-driver.md)。

可以调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 和 [**SetupDiSetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdevicepropertyw) 检索和设置 DEVPKEY_Device_LowerFilters 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_LowerFilters 属性键。 相反，你可以使用相应的 SPDRP_LOWERFILTERS 标识符来访问这些早期版本的 Windows 上的属性值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅 [SPDRP_Xxx 属性访问设备实例](./accessing-device-instance-spdrp-xxx-properties.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

