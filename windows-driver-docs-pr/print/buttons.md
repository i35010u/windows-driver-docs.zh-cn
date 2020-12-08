---
title: 按钮元素
description: 必需的按钮元素指定客户端计算机上的事件通知消息框中显示的一个或多个按钮。
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
ms.openlocfilehash: 628c98e10f4cdabdc9247300893ff5e22c6f241d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797739"
---
# <a name="buttons-element"></a>按钮元素

必需的 **按钮** 元素指定客户端计算机上的事件通知消息框中显示的一个或多个按钮。

在 *asyncui* 命名空间中的此 URI 处定义了 **按钮** 元素：

```xml
https://schemas.microsoft.com/2003/print/asyncui/v1/request
```

此资源可能在某些语言和国家/地区不可用。

## <a name="usage"></a>使用情况

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

有关演示如何使用 button 元素将显示 **"确定" 和 "** **取消**" 按钮的两个 **按钮** 元素括 **起来的代码** 示例，请参阅 [**按钮**](button.md)。

## <a name="see-also"></a>请参阅

[鼠标](button.md)

[messageBoxUI](messageboxui.md)
