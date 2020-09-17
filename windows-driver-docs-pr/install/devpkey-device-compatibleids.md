---
title: DEVPKEY_Device_CompatibleIds
description: DEVPKEY_Device_CompatibleIds
ms.assetid: 01858541-9239-48be-8c48-ee163d87e767
keywords:
- DEVPKEY_Device_CompatibleIds 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_CompatibleIds
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cdd1f4f3a58b466bab95c57fe5f3eb66792c5d6c
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90717092"
---
# <a name="devpkey_device_compatibleids"></a>DEVPKEY_Device_CompatibleIds


DEVPKEY_DEVICE_CompatibleIds 设备属性表示设备实例的兼容标识符的列表。

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
<td align="left"><p>DEVPKEY_Device_CompatibleIds</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>内部数据格式</strong></p></td>
<td align="left">"<em>兼容-id1</em>\ 0<em>兼容-id</em>2 \ 0 ..."<em>兼容-idn</em>\ 0 \ 0 "</td>
</tr>
<tr class="even">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>对应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_COMPATIBLEIDS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_DEVICE_CompatibleIds 的值由在安装设备的 INF 文件的 " [**Inf 模型" 部分**](./inf-models-section.md)中为设备提供的*兼容 id*输入值设置。

可以调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_DEVICE_CompatibleIds 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_CompatibleIds 属性键。 相反，你可以使用相应的 SPDRP_COMPATIBLEIDS 标识符来访问这些早期版本的 Windows 上的属性值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅 [SPDRP_Xxx 属性访问设备实例](./accessing-device-instance-spdrp-xxx-properties.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**INF Models 节**](./inf-models-section.md)

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

