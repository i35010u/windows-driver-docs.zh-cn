---
title: Const (WSD)
description: 用于设备 (WSD) Const 构造的 Web 服务定义必须返回的数据类型和值。
keywords:
- Const 构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec2f1fbf5dd1e63030d6da5cfcdf98777d6cd415
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797565"
---
# <a name="const-wsd"></a>Const (WSD)


用于设备 (WSD) Const 构造的 Web 服务定义必须返回的数据类型和值。 Const 用于不在值中更改的元素。 Const 构造是在 WsdBidi 中定义的。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>name</p></td>
<td><p>架构值的名称。</p></td>
</tr>
<tr class="even">
<td><p>type</p></td>
<td><p><strong>值</strong>特性中的数据类型， <a href="/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](/windows-hardware/drivers/ddi/winspool/ne-winspool-bidi_type)"><strong>BIDI_TYPE</strong></a>枚举中的值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>value</strong></p></td>
<td><p>包含常量值的字符串。</p></td>
</tr>
</tbody>
</table>

 

### <a name="code-example"></a>代码示例

下面的代码示例返回一个常数值，该常量值已在特定双向架构查询的双向扩展文件中定义。

```cpp
<Property name="Printer">
  <Property name="Extension">
    <Const name="Version" type="BIDI_INT">1</Const>
  </Property>
</Property>
```

此示例将生成以下查询：

```cpp
\Printer.Extension.Version:1
```

