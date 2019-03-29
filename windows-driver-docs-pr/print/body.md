---
title: body 元素
description: 所需的正文元素提供的文本显示在事件通知消息。 此文本应提供用户有关打印机事件的特定详细信息。
ms.assetid: 3343c272-5090-4b60-ab04-08038d2583ff
keywords:
- 正文元素打印设备
topic_type:
- apiref
api_name:
- body
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f252d61cb1d699a0804e957d0a23726ccd404bbc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568221"
---
# <a name="body-element"></a>body 元素


所需**正文**元素提供的文本显示在事件通知消息。 此文本应提供用户有关打印机事件的特定详细信息。

**正文**中定义元素*asyncui*此 URI 处的命名空间： http://schemas.microsoft.com/2003/print/asyncui/v1/request。 （此资源可能不会在某些语言和国家/地区中可用。）

<a name="usage"></a>用法
-----

```xml
<body
  stringID = "xs:string"
  resourceDll = "xs:string">
  child elements
</body>
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
<td><p><strong>resourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>一个指定的资源 DLL，其中包含要显示在事件通知消息的正文文本的可选属性。 此 DLL 应是打印机驱动程序的依赖文件和驱动程序资源文件夹 （例如，%systemroot%\system32\spool\drivers\w32x86\3) 中必须存在。</p></td>
</tr>
<tr class="even">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>指定要在事件通知消息的正文中显示的文本的所需的属性。 属性值的资源 DLL 中指定的文本字符串的位置。</p></td>
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
<p>可选元素，它指定文本字符串正文文本规范中的参数的替代。</p></td>
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
<p>一个用于客户端计算机上显示消息气泡的可选元素。</p></td>
</tr>
<tr class="even">
<td><p><a href="messageboxui.md" data-raw-source="[&lt;strong&gt;messageBoxUI&lt;/strong&gt;](messageboxui.md)"><strong>messageBoxUI</strong></a></p></td>
<td><p></p>
<p>可选元素，它用于在客户端计算机上显示一个消息框。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

从资源 DLL 加载的正文文本可以包含百分比 （%）将替换为文本字符串由指定的标记[**参数**](parameter.md)子元素。

多个**正文**，可以使用标记按顺序，在这种情况下每个生成的文本将串联事件通知消息中。 将文本字符串的每个对之间插入一个空格。 同时，可以显示相同的通知消息： 状态信息，如"您的打印机是超出手写内容。"，并指示用户，如"更换墨盒和以继续在打印机上按继续按钮。

中包含的文本**正文**元素应让用户知道哪些操作才可用。

使用以下建议有用且简洁保持消息文本：

-   使用完整的句子结束标点。
-   编写可本地化为其他语言时少于 255 个字符的正文文本。 例如，在英语中的一条消息通常不应使用超过 200 个字符以适应本地化为其他语言。
-   包括允许用户完成所请求的操作，如特定的对象名称、 用户名、 文件名称或 Url 的基本信息。 用户应该不需要打开另一个窗口来查找此类信息。
-   将对象名称 (例如，"纸张 Bin 1") 的前后的双引号。 当对象名称使用首字母大写的单词，但是，不要使用引号用户名，例如它的偏移量以冒号 (例如，打印机名称：我的打印机），或从上下文可轻松地确定。
-   如果需要截断为固定的最大大小以适应本地化的对象名称，使用省略号 （...） 以指示截断。
-   如果为用户执行任何操作，一条通知消息提供了一个按钮，请确保有消息信息与按钮之间的 2 个换行符。 使用简单的面向操作的短语，例如，"单击到重新启动打印，"或"单击以查看详细信息。"按钮的标签
-   只能使用通知消息，用户可以自由地忽略的非关键信息。 正文文本不应显示用户必须执行的操作。
-   如果用户应执行的操作，明确描述的重要性和后果的执行操作。
-   描述平实的语言中包含的有关用户如何修复此问题的特定信息的问题。
-   描述与用户相关的方式中的事件。 如果用户能执行的任务或更改作为通知结果的行为可能相关通知消息。
-   描述根据用户目标而不是在由于技术问题方面的事件。

<a name="examples"></a>示例
--------

下面的代码示例演示如何使用**正文**元素。

```xml
<?xml version="1.0" ?>
   <asyncPrintUIRequest
    xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/request">
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

## <a name="see-also"></a>请参阅

[balloonUI](balloonui.md)

[messageBoxUI](messageboxui.md)

[parameter](parameter.md)
