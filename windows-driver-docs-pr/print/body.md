---
title: body 元素
description: 必需的 body 元素提供在事件通知消息中显示的文本。 此文本应提供有关打印机事件的用户特定详细信息。
ms.assetid: 3343c272-5090-4b60-ab04-08038d2583ff
keywords:
- body 元素打印设备
topic_type:
- apiref
api_name:
- body
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61da9d170f9a90f078296677893aaddda49f49f8
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652864"
---
# <a name="body-element"></a>body 元素

必需的**body**元素提供在事件通知消息中显示的文本。 此文本应提供有关打印机事件的用户特定详细信息。

**Body**元素在*asyncui*命名空间中的此 URI 上定义： [https://schemas.microsoft.com/2003/print/asyncui/v1/request](https://schemas.microsoft.com/2003/print/asyncui/v1/request)。 （此资源可能在某些语言和国家/地区不可用。）

## <a name="usage"></a>Usage

```xml
<body
  stringID = "xs:string"
  resourceDll = "xs:string">
  child elements
</body>
```

## <a name="attributes"></a>属性

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
<td><p><strong>resourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>无</p></td>
<td><p></p>
<p>一个可选属性，它指定一个资源 DLL，其中包含要在事件通知消息中显示的正文文本。 此 DLL 应是打印机驱动程序的依赖文件，并且必须位于驱动程序资源文件夹中（例如，%SYSTEMROOT%\system32\spool\drivers\w32x86\3）。</p></td>
</tr>
<tr class="even">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>“是”</p></td>
<td><p></p>
<p>一个必需的属性，指定要在事件通知消息正文中显示的文本。 属性值指定资源 DLL 中文本字符串的位置。</p></td>
</tr>
</tbody>
</table>

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
<td><p><a href="parameter.md" data-raw-source="[&lt;strong&gt;parameter&lt;/strong&gt;](parameter.md)"><strong>parameter</strong></a></p></td>
<td><p></p>
<p>一个可选元素，该元素指定替换正文文本规范中的参数的文本字符串。</p></td>
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
<td><p><a href="balloonui.md" data-raw-source="[&lt;strong&gt;balloonUI&lt;/strong&gt;](balloonui.md)"><strong>balloonUI</strong></a></p></td>
<td><p></p>
<p>一个可选元素，用于在客户端计算机上显示消息气球。</p></td>
</tr>
<tr class="even">
<td><p><a href="messageboxui.md" data-raw-source="[&lt;strong&gt;messageBoxUI&lt;/strong&gt;](messageboxui.md)"><strong>messageBoxUI</strong></a></p></td>
<td><p></p>
<p>一个可选元素，用于在客户端计算机上显示消息框。</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>备注

从资源 DLL 加载的正文文本可以包含百分比（%）将替换为[**参数**](parameter.md)子元素所指定的文本字符串的标记。

可以按顺序使用多个正文标记，在这种情况下，将在事件通知消息中连接每个**正文**标记所生成的文本。 将在每个文本字符串对之间插入空格。 同一通知消息可以同时显示这两种信息：状态信息（如 "打印机已用尽墨）" 和用户说明，如 "更换墨盒并按下打印机上的恢复按钮" 以继续操作。

**Body**元素中包含的文本应允许用户了解可用的操作。

使用以下建议使消息文本非常有用和简洁：

- 使用带有结束标点的完整句子。
- 当本地化为其他语言时，请撰写可小于255个字符的正文文本。 例如，使用英语的消息通常不应使用超过200个字符，以适应其他语言的本地化。
- 包括允许用户完成请求的操作的基本信息，例如特定的对象名称、用户名、文件名或 Url。 用户应该不需要打开另一个窗口即可找到此类信息。
- 用双引号将对象名称括起来（例如，"纸盒 1"）。 但是，当对象名称使用大写的单词（例如用户名）时，请不要使用引号，而是使用冒号（例如，打印机名称： My printer）偏移，或者可以通过上下文轻松确定。
- 如果必须将对象名称截断为固定的最大大小以适应本地化，请使用省略号（...）指示截断。
- 如果通知消息提供用户操作按钮，请确保消息信息和按钮之间有两个换行符。 用简单的面向操作的短语标记按钮，如 "单击以重新开始打印" 或单击 "查看详细信息"。
- 仅对用户可以自由忽略的非关键信息使用通知消息。 正文文本不应说明用户必须执行某一操作。
- 如果用户应执行某个操作，请清楚地描述执行该操作的重要性和后果。
- 以普通语言描述问题，并提供有关用户如何解决此问题的具体信息。
- 以与用户相关的方式描述事件。 如果用户将执行任务或更改行为作为通知的结果，则通知消息是相关的。
- 描述用户目标而不是技术问题方面的事件。

## <a name="examples"></a>示例

下面的代码示例演示如何使用**body**元素。

```xml
<?xml version="1.0" ?>
   <asyncPrintUIRequest
    xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/request">
    <v1>
      <requestOpen>
        <balloonUI iconID="1" resourceDll="IHV.dll">
          <title stringID="1234" resourceDll="IHV.dll" />
          <body stringID="100" resourceDll="IHV.dll">
            <parameter stringID="5" />
            <parameter stringID="1002" resourceDll="IHV.dll" />
          </body>
        </balloonUI>
      </requestOpen>
    </v1>
  </asyncPrintUIRequest>
```

## <a name="see-also"></a>另请参阅

[balloonUI](balloonui.md)

[messageBoxUI](messageboxui.md)

[parameter](parameter.md)
