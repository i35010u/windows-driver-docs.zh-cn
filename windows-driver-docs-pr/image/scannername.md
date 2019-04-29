---
title: ScannerName 元素
description: 所需的 ScannerName 元素指定扫描程序以管理方式分配的用户友好的名称。
ms.assetid: 013a1cb8-4b59-4271-a7bd-eb8d741643e5
keywords:
- ScannerName 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScannerName xml lang "..."
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59349e620d90ac2187fc194b139a8d51ed9cfaed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370069"
---
# <a name="scannername-element"></a>ScannerName 元素


所需**ScannerName**元素指定的扫描程序以管理方式分配的用户友好名称。

<a name="usage"></a>用法
-----

```xml
<wscn:ScannerName xml:lang="..."
  lang = "xs:string">
  text
</wscn:ScannerName xml:lang="...">
```

<a name="attributes"></a>特性
----------

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>在任务栏的搜索框中键入</th>
<th>必需</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><strong>lang</strong></strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>（可选）标识的字符串的字符串指定的语言的字符字符串。<em>字符串</em></p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>文本值
----------

指定扫描程序的用户友好名称的字符串。

## <a name="child-elements"></a>子元素


没有子元素。

## <a name="parent-elements"></a>父元素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="scannerdescription.md" data-raw-source="[&lt;strong&gt;ScannerDescription&lt;/strong&gt;](scannerdescription.md)"><strong>ScannerDescription</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

配置**ScannerName**元素的值是特定于实现的; 例如，您可以配置扫描程序的本地控制台或设备的 web 服务器通过此值。 如果设备具有只有一个托管的服务，其友好名称和**ScannerName**元素应具有相同的值。 如果设备包含多个托管的服务， **ScannerName**应确定扫描程序。

扫描设备可以返回此元素中使用启用对多个本地化语言的支持的多个版本**xml: lang**属性。

<a name="examples"></a>示例
--------

以下代码示例演示如何使用 ScannerName 元素。

```xml
<wscn:ScannerName xml:lang="en-AU, en-CA, en-GB, en-US">
  Accounting Scanner in Copy Room 2
</wscn:ScannerName>
```

## <a name="see-also"></a>请参阅

[**ScannerDescription**](scannerdescription.md)
