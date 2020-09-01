---
title: DEVPKEY_Device_DriverDesc
description: DEVPKEY_Device_DriverDesc
ms.assetid: abe484ec-f9f8-4f22-b18b-64ffb88a94a2
keywords:
- DEVPKEY_Device_DriverDesc 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DriverDesc
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 85e277b1b00191c8ff8baf229a286f00d478bbd0
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097387"
---
# <a name="devpkey_device_driverdesc"></a>DEVPKEY_Device_DriverDesc


DEVPKEY_Device_DriverDesc 设备属性表示为设备实例安装的驱动程序的说明。

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
<td align="left"><p>DEVPKEY_Device_DriverDesc</p></td>
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
<td align="left"><p><strong>对应的注册表值标识符和注册表值名称</strong></p></td>
<td align="left"><p>REGSTR_VAL_DRVDESC</p>
<p><strong>DriverDesc</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_DriverDesc 的值由安装设备的 INF 文件的 " [**Inf*模型*" 部分**](./inf-models-section.md)提供的*设备说明*条目值设置。

DEVPKEY_Device_DriverDesc 的值不会显示在最终用户对话框中，也不会出于操作系统的任何原因而使用。

可以调用 [**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_Device_DriverDesc 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_LocationPaths 属性键。 在这些早期版本的 Windows 上，可以通过访问设备实例的软件密钥下的相应 **DriverDesc** 注册表值来访问此属性的值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅 [访问设备驱动程序属性](./accessing-device-driver-properties.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>另请参阅


[**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

