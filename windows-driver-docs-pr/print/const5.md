---
title: Const (WSD)
description: Web Services for Devices (WSD) Const 构造定义数据类型和值，必须返回该值。
ms.assetid: e9bcf007-0117-48a9-9873-a9bbc5702e29
keywords:
- Const 构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a1c26fa8413e64461e7c61bf4ae068521a482e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384502"
---
# <a name="const-wsd"></a>Const (WSD)


Web Services for Devices (WSD) Const 构造定义数据类型和值，必须返回该值。 常量用于不更改值中的元素。 Const 构造 WsdBidi.xsd 中定义。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>名称</strong></p></td>
<td><p>架构值的名称。</p></td>
</tr>
<tr class="even">
<td><p><strong>type</strong></p></td>
<td><p>中的数据类型<strong>值</strong>属性中的值<a href="https://msdn.microsoft.com/library/windows/hardware/ff545211" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545211)"> <strong>BIDI_TYPE</strong> </a>枚举。</p></td>
</tr>
<tr class="odd">
<td><p><strong>value</strong></p></td>
<td><p>包含的常量值的字符串。</p></td>
</tr>
</tbody>
</table>

 

### <a name="code-example"></a>代码示例

下面的代码示例返回有关特定 bidi 架构查询 bidi 扩展文件中定义的常量值。

```cpp
<Property name="Printer">
  <Property name="Extension">
    <Const name="Version" type="BIDI_INT">1</Const>
  </Property>
</Property>
```

此示例将返回在下面的查询：

```cpp
\Printer.Extension.Version:1
```

 

 




