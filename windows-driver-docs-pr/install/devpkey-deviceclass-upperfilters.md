---
title: DEVPKEY_DeviceClass_UpperFilters
description: DEVPKEY_DeviceClass_UpperFilters
ms.assetid: 9a6a9587-340c-460e-b6e2-1aadfb5b8c2f
keywords:
- DEVPKEY_DeviceClass_UpperFilters 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_UpperFilters
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6c34d8203c9dd3b3b871c6aad1b97f29a4f6dd48
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716390"
---
# <a name="devpkey_deviceclass_upperfilters"></a>DEVPKEY_DeviceClass_UpperFilters


DEVPKEY_DeviceClass_UpperFilters 设备属性表示为 [设备安装程序类](./overview-of-device-setup-classes.md)安装的顶级筛选器驱动程序的服务名称列表。

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
<td align="left"><p>DEVPKEY_DeviceClass_UpperFilters</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据格式</strong></p></td>
<td align="left"><p>"<em>服务-name1</em>\ 0<em>服务-name2</em>\ 0 .。。<em>nameN</em>\ 0 \ 0 "</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装类筛选器后由安装应用程序和安装程序进行的只读访问</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>对应 SPCRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPCRP_UPPERFILTERS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应的注册表值名称</strong></p></td>
<td align="left"><p><strong>UpperFilters</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

安装类筛选器驱动程序时，将设置 DEVPKEY_DeviceClass_UpperFilters 的值。 有关如何安装类筛选器驱动程序的详细信息，请参阅 [安装筛选器驱动程序](./installing-a-filter-driver.md) 和 [**INF ClassInstall32 部分**](./inf-classinstall32-section.md)。

可以调用 [**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw) 或 [**SetupDiGetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyexw) 来检索 DEVPKEY_DeviceClass_UpperFilters 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_DeviceClass_UpperFilters 属性键。 在这些早期版本的 Windows 上，可以通过访问类注册表项下的相应 **UpperFilters** 注册表值访问此属性的值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅 [访问类注册表项下的注册表项值](./accessing-registry-entry-values-under-the-class-registry-key.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**INF ClassInstall32 节**](./inf-classinstall32-section.md)

[**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

[**SetupDiOpenClassRegKeyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)

 

