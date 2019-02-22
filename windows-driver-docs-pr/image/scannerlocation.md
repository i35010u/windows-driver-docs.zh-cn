---
title: ScannerLocation 元素
description: 可选 ScannerLocation 元素指定扫描程序以管理方式分配的的位置。
ms.assetid: 564a468d-7a4a-49c6-921a-5d8825c783fb
keywords:
- ScannerLocation 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScannerLocation xml lang "..."
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8107024dc1c0215a94a4a606062b6a7ed2c1cd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525160"
---
# <a name="scannerlocation-element"></a>ScannerLocation 元素


可选**ScannerLocation**元素指定的扫描程序以管理方式分配的位置。

<a name="usage"></a>用法
-----

```xml
<wscn:ScannerLocation xml:lang="..."
  lang = "xs:string">
  text
</wscn:ScannerLocation xml:lang="...">
```

<a name="attributes"></a>属性
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
<th>属性</th>
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

指定扫描程序的位置的字符串。

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

配置**ScannerLocation**元素的值是特定于实现的; 例如，您可以配置扫描程序的本地控制台或设备的 web 服务器通过此值。 扫描设备可以返回此元素中使用启用对多个本地化语言的支持的多个版本**xml: lang**属性。

<a name="examples"></a>示例
--------

以下代码示例演示如何使用 ScannerLocation 元素。

```xml
<wscn:ScannerLocation xml:lang="en-AU, en-CA, en-GB, en-US">
  LA Campus - Building 1
</wscn:ScannerLocation>
```

## <a name="see-also"></a>另请参阅

[**ScannerDescription**](scannerdescription.md)
