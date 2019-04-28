---
title: Buttons 元素
description: 必需的按钮元素指定一个或多个按钮，在事件通知消息框上显示客户端计算机。
ms.assetid: bf3718c0-37d9-4b73-a015-8a5a95535381
keywords:
- 按钮元素打印设备
topic_type:
- apiref
api_name:
- buttons
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7e40fb775bd3f68c4de1e5d5821f1610981483d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330452"
---
# <a name="buttons-element"></a>Buttons 元素


所需**按钮**元素指定一个或多个按钮，在事件通知消息框上显示客户端计算机。

**按钮**中定义元素*asyncui*此 URI 处的命名空间： http://schemas.microsoft.com/2003/print/asyncui/v1/request。 （此资源可能不会在某些语言和国家/地区中可用。）

<a name="usage"></a>用法
-----

```xml
<buttons>
  child elements
</buttons>
```

<a name="attributes"></a>特性
----------

没有特性。

## <a name="child-elements"></a>子元素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="button.md" data-raw-source="[&lt;strong&gt;button&lt;/strong&gt;](button.md)"><strong>button</strong></a></p></td>
<td><p></p>
<p>在客户端计算机显示一个消息框中指定的一个按钮特性所必需的元素。</p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="messageboxui.md" data-raw-source="[&lt;strong&gt;messageBoxUI&lt;/strong&gt;](messageboxui.md)"><strong>messageBoxUI</strong></a></p></td>
<td><p></p>
<p>可选元素，它用于在客户端计算机上显示一个消息框。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

请参阅[**按钮**](button.md)用于演示如何使用代码如示例**按钮**元素需要包含两个**按钮**显示的元素**确定**和一个**取消**按钮。

## <a name="see-also"></a>请参阅

[button](button.md)

[messageBoxUI](messageboxui.md)
