---
title: Const (WSD)
description: Web Services for Devices (WSD) Const 构造定义数据类型和值，必须返回该值。
ms.assetid: e9bcf007-0117-48a9-9873-a9bbc5702e29
keywords:
- Const 构造
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 608c8b54be0dde51b37b1117366428f7c328d4b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374675"
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
<td><p><strong>name</strong></p></td>
<td><p>架构值的名称。</p></td>
</tr>
<tr class="even">
<td><p><strong>type</strong></p></td>
<td><p>中的数据类型<strong>值</strong>属性中的值<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/ne-winspool-bidi_type" data-raw-source="[&lt;strong&gt;BIDI_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winspool/ne-winspool-bidi_type)"> <strong>BIDI_TYPE</strong> </a>枚举。</p></td>
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

 

 




