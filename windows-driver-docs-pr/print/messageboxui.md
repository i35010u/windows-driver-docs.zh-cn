---
title: messageBoxUI 元素
description: 可选的 messageBoxUI 元素用于在客户端计算机上显示消息框。
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
ms.openlocfilehash: da6e80d28e2e23d2a41b1da3ff632de81e2899e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807875"
---
# <a name="messageboxui-element"></a>messageBoxUI 元素

可选的 **messageBoxUI** 元素用于在客户端计算机上显示消息框。

**MessageBoxUI** 元素在 *asyncui* 命名空间中的此 URI 处定义：

```xml
https://schemas.microsoft.com/2003/print/asyncui/v1/request
```

此资源可能在某些语言和国家/地区不可用。

## <a name="usage"></a>使用情况

```xml
<messageBoxUI>
  child elements
</messageBoxUI>
```

## <a name="attributes"></a>特性

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
<td><p><a href="bitmap.md" data-raw-source="[&lt;strong&gt;bitmap&lt;/strong&gt;](bitmap.md)"><strong>图</strong></a></p></td>
<td><p></p>
<p>一个可选元素，用于在消息框中将位图图像显示在正文文本的左侧。</p></td>
</tr>
<tr class="even">
<td><p><a href="body.md" data-raw-source="[&lt;strong&gt;body&lt;/strong&gt;](body.md)"><strong>body</strong></a></p></td>
<td><p></p>
<p>一个必需的元素，它提供在事件通知消息中显示的文本。 此文本应提供有关打印机事件的用户特定详细信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="buttons.md" data-raw-source="[&lt;strong&gt;buttons&lt;/strong&gt;](buttons.md)"><strong>按钮</strong></a></p></td>
<td><p></p>
<p>一个必需的元素，该元素指定客户端计算机上的事件通知消息框中显示的一个或多个按钮。</p></td>
</tr>
<tr class="even">
<td><p><a href="title.md" data-raw-source="[&lt;strong&gt;title&lt;/strong&gt;](title.md)"><strong>title</strong></a></p></td>
<td><p></p>
<p>一个必需的元素，该元素提供在事件通知消息标题中显示的文本。</p></td>
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
<p>用于在客户端计算机上打开事件通知消息的元素。</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>备注

有关显示如何将 **"确定"** 按钮和 "**取消**" 按钮设置为消息框的代码示例，请参阅 [**按钮**](button.md)。 请参阅 " **示例** " 部分，了解有关如何捕获按钮-单击消息框的信息。

## <a name="examples"></a>示例

下面的代码示例演示如何通知打印机驱动程序，消息框中已单击 **"确定"** 按钮。

```xml
<?xml version="1.0" ?> 
  <asyncPrintUIResponse xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/response">
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

[位图](bitmap.md)

[body](body.md)

[鼠标](button.md)

[buttons](buttons.md)

[requestOpen](requestopen.md)

[title](title.md)
