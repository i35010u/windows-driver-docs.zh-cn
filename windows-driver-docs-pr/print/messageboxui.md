---
title: messageBoxUI 元素
description: 可选 messageBoxUI 元素用于在客户端计算机上显示一个消息框。
ms.assetid: 83fe67fe-72b0-42e2-864e-242b7b9989d9
keywords:
- messageBoxUI 元素打印设备
topic_type:
- apiref
api_name:
- messageBoxUI
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 070b4cd8840d777e49b035e5858a819244da0c24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568819"
---
# <a name="messageboxui-element"></a>messageBoxUI 元素


可选**messageBoxUI**元素用于在客户端计算机上显示一个消息框。

**MessageBoxUI**中定义元素*asyncui*此 URI 处的命名空间： http://schemas.microsoft.com/2003/print/asyncui/v1/request。 （此资源可能不会在某些语言和国家/地区中可用。）

<a name="usage"></a>用法
-----

```xml
<messageBoxUI>
  child elements
</messageBoxUI>
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
<td><p><a href="bitmap.md" data-raw-source="[&lt;strong&gt;bitmap&lt;/strong&gt;](bitmap.md)"><strong>bitmap</strong></a></p></td>
<td><p></p>
<p>一个用于消息框中的正文文本的左侧显示位图图像的可选元素。</p></td>
</tr>
<tr class="even">
<td><p><a href="body.md" data-raw-source="[&lt;strong&gt;body&lt;/strong&gt;](body.md)"><strong>body</strong></a></p></td>
<td><p></p>
<p>提供的文本的所需的元素显示在事件通知消息。 此文本应提供用户有关打印机事件的特定详细信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="buttons.md" data-raw-source="[&lt;strong&gt;buttons&lt;/strong&gt;](buttons.md)"><strong>buttons</strong></a></p></td>
<td><p></p>
<p>必需的元素，用于指定一个或多个按钮的显示客户端计算机上的事件中的通知消息框。</p></td>
</tr>
<tr class="even">
<td><p><a href="title.md" data-raw-source="[&lt;strong&gt;title&lt;/strong&gt;](title.md)"><strong>title</strong></a></p></td>
<td><p></p>
<p>提供事件通知消息的标题中显示的文本所必需的元素。</p></td>
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
<td><p><a href="requestopen.md" data-raw-source="[&lt;strong&gt;requestOpen&lt;/strong&gt;](requestopen.md)"><strong>requestOpen</strong></a></p></td>
<td><p></p>
<p>一个用于打开客户端计算机上的事件通知消息的元素。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

请参阅[**按钮**](button.md)有关代码示例演示如何将放置**确定**按钮和一个**取消**按钮的消息框。 请参阅**示例**部分，了解有关如何捕获按钮单击消息框上的信息。

<a name="examples"></a>示例
--------

下面的代码示例演示如何通知打印机驱动程序的**确定**消息框上单击了按钮。

```xml
<?xml version="1.0" ?> 
  <asyncPrintUIResponse xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/response">
    <v1>
      <requestClose>
        <messageBoxUI>
          <buttonID>IDOK</buttonID>
        </messageBoxUI >
      </requestClose>
    </v1>
  </asyncPrintUIResponse>
```

## <a name="see-also"></a>请参阅

[bitmap](bitmap.md)

[body](body.md)

[button](button.md)

[buttons](buttons.md)

[requestOpen](requestopen.md)

[title](title.md)
