---
title: 按钮元素
description: 必需的按钮元素指定客户端计算机上的事件通知消息框中显示的一个或多个按钮。
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
ms.openlocfilehash: 2b1c28d43efafeab6892f6029200a7daf1024479
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652860"
---
# <a name="buttons-element"></a>按钮元素


必需的**按钮**元素指定客户端计算机上的事件通知消息框中显示的一个或多个按钮。

在*asyncui*命名空间中的此 URI 处定义了 "**按钮**" 元素： [https://schemas.microsoft.com/2003/print/asyncui/v1/request](https://schemas.microsoft.com/2003/print/asyncui/v1/request)。 （此资源可能在某些语言和国家/地区不可用。）

<a name="usage"></a>Usage
-----

```xml
<buttons>
  child elements
</buttons>
```

<a name="attributes"></a>属性
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
<td><p><a href="button.md" data-raw-source="[&lt;strong&gt;button&lt;/strong&gt;](button.md)"><strong>鼠标</strong></a></p></td>
<td><p></p>
<p>一个必需的元素，它指定在客户端计算机上显示的消息框中的按钮特性。</p></td>
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
<p>一个可选元素，用于在客户端计算机上显示消息框。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

有关演示如何使用 button 元素将显示 **"确定" 和 "** **取消**" 按钮的两个**按钮**元素括**起来的代码**示例，请参阅[**按钮**](button.md)。

## <a name="see-also"></a>另请参阅

[button](button.md)

[messageBoxUI](messageboxui.md)
