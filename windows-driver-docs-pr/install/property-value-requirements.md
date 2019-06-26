---
title: 属性值要求
description: 属性值要求
ms.assetid: 05512f3d-fe64-4de0-848c-c983d883fc60
keywords:
- 设备属性 WDK 设备安装，属性值要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 719a8ce9d66c84a73f9ad2fb9e7e9bbafc6172a3
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393475"
---
# <a name="property-value-requirements"></a>属性值要求


Windows 强制执行下表中列出的设备属性值大小要求。 Windows 仅设置设备属性值，如果设备属性值符合这些值的大小要求。

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
<td align="left"><p>固定长度<a href="https://docs.microsoft.com/previous-versions/ff537793(v=vs.85)" data-raw-source="[&lt;strong&gt;base-data-type&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff537793(v=vs.85))"><strong>基本数据类型</strong></a>值</p></td>
<td align="left"><p>所提供的数据的指定的大小必须是基本数据类型中的字节数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>固定长度数据的基本类型值的数组</p></td>
<td align="left"><p>所提供的数据的指定的大小必须是数组的零个或多个基数据类型值的字节数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>一个<a href="https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-security-descriptor" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_SECURITY_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-security-descriptor)"> <strong>DEVPROP_TYPE_SECURITY_DESCRIPTOR</strong> </a>数据类型的值</p></td>
<td align="left"><p>所提供的数据的指定的大小必须是一个可变长度自相关 SECURITY_DESCRIPTOR 结构的字节数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>一个<a href="https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-string" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-string)"> <strong>DEVPROP_TYPE_STRING</strong> </a>数据类型的值， <a href="https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-security-descriptor-string" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-security-descriptor-string)"> <strong>DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING</strong> </a>数据类型值或<a href="https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-string-indirect" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_INDIRECT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-string-indirect)"> <strong>DEVPROP_TYPE_STRING_INDIRECT</strong> </a>数据类型的值</p></td>
<td align="left"><p>所提供的数据的指定的大小必须为 Unicode 的字节数<a href="https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types" data-raw-source="[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)">REG_SZ</a>包括 NULL 终止符的字符串。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEVPROP_TYPE_STRING 类型字符串的列表、 一系列 DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING 键入字符串或 DEVPROP_TYPE_STRING_LIST 数据类型值</p></td>
<td align="left"><p>所提供的数据的指定的大小必须是 Unicode REG_MULTLI_SZ 列表的字符串，其中包括最后一个 NULL 终止符的终止字符串列表的字节数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>所有属性值</p></td>
<td align="left"><p>除了此表中的其他行中列出的属性值大小要求，最大大小 （字节） 的属性值是 UNICODE_STRING_MAX_BYTES。</p></td>
</tr>
</tbody>
</table>

 

 

 





