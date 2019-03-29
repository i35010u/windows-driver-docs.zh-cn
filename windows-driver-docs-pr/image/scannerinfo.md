---
title: ScannerInfo 元素
description: 可选 ScannerInfo 元素包含任何系统管理分配有关扫描程序的描述性信息。
ms.assetid: 41d31209-8269-42ef-99f2-83818eb06f6b
keywords:
- ScannerInfo 元素成像设备
topic_type:
- apiref
api_name:
- wscn ScannerInfo xml lang "..."
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 245bde98b14365c3a5e619447d2a751540070d8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566120"
---
# <a name="scannerinfo-element"></a>ScannerInfo 元素


可选**ScannerInfo**元素包含任何系统管理分配有关扫描程序的描述性信息。

<a name="usage"></a>用法
-----

```xml
<wscn:ScannerInfo xml:lang="..."
  lang = "xs:string">
  text
</wscn:ScannerInfo xml:lang="...">
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

提供有关扫描程序的描述性信息的字符串。

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

配置**ScannerInfo**元素的值是特定于实现的; 例如，您可以配置扫描程序的本地控制台或设备的 web 服务器通过此值。 扫描设备可以返回此元素中使用启用对多个本地化语言的支持的多个版本**xml: lang**属性。

<a name="examples"></a>示例
--------

以下代码示例演示如何使用 ScannerInfo 元素。

```xml
<wscn:ScannerInfo xml:lang="en-AU, en-CA, en-GB, en-US">
  Out of courtesy to others, please scan only
  small (1-5 page) jobs at this scanner.
</wscn:ScannerInfo>
```

## <a name="see-also"></a>请参阅

Description**](scannerdescription.md)
