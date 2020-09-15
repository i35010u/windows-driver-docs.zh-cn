---
title: 属性值要求
description: 属性值要求
ms.assetid: 05512f3d-fe64-4de0-848c-c983d883fc60
keywords:
- 设备属性 WDK 设备安装，属性值要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e343e5dcfbbdb5178d6141d1a9a37311dbaefe0
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104104"
---
# <a name="property-value-requirements"></a>属性值要求


Windows 强制执行下表中列出的设备属性值大小要求。 如果设备属性值符合这些值大小要求，则 Windows 仅设置设备属性值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性数据类型</th>
<th align="left">属性值大小要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>固定长度的 <a href="/previous-versions/ff537793(v=vs.85)" data-raw-source="[&lt;strong&gt;base-data-type&lt;/strong&gt;](/previous-versions/ff537793(v=vs.85))"><strong>基本数据类型</strong></a> 值</p></td>
<td align="left"><p>提供的数据的指定大小必须是基本数据类型中的字节数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>固定长度的基本数据类型值的数组</p></td>
<td align="left"><p>提供的数据的指定大小必须是零个或多个基数据类型值的数组的字节数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>一个 <a href="/windows-hardware/drivers/install/devprop-type-security-descriptor" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_SECURITY_DESCRIPTOR&lt;/strong&gt;](./devprop-type-security-descriptor.md)"><strong>DEVPROP_TYPE_SECURITY_DESCRIPTOR</strong></a> 数据类型值</p></td>
<td align="left"><p>提供的数据的指定大小必须为可变长度、自相关 SECURITY_DESCRIPTOR 结构的字节数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/install/devprop-type-string" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](./devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a>数据类型值、 <a href="/windows-hardware/drivers/install/devprop-type-security-descriptor-string" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING&lt;/strong&gt;](./devprop-type-security-descriptor-string.md)"><strong>DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING</strong></a>数据类型值或<a href="/windows-hardware/drivers/install/devprop-type-string-indirect" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_INDIRECT&lt;/strong&gt;](./devprop-type-string-indirect.md)"><strong>DEVPROP_TYPE_STRING_INDIRECT</strong></a>数据类型值</p></td>
<td align="left"><p>提供的数据的指定大小必须是 Unicode <a href="/windows/desktop/SysInfo/registry-value-types" data-raw-source="[REG_SZ](/windows/desktop/SysInfo/registry-value-types)">REG_SZ</a> 字符串的字节数，包括 NULL 终止符。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEVPROP_TYPE_STRING 类型字符串的列表、DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING 类型字符串的列表或 DEVPROP_TYPE_STRING_LIST 数据类型值</p></td>
<td align="left"><p>提供的数据的指定大小必须是 Unicode REG_MULTLI_SZ 字符串列表的字节数，包括终止字符串列表的最终 NULL 终止符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>所有属性值</p></td>
<td align="left"><p>除了在此表的其他行中列出的属性值大小要求外，UNICODE_STRING_MAX_BYTES 属性值的最大大小（以字节为单位）。</p></td>
</tr>
</tbody>
</table>

 

