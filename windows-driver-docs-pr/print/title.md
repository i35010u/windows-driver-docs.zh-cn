---
title: title 元素
description: 所需的标题元素提供事件通知消息的标题中显示的文本。
ms.assetid: 60583593-9fe9-4c3c-ab86-3e7c37a8e199
keywords:
- 标题元素打印设备
topic_type:
- apiref
api_name:
- title
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: acbf9669af62899138560270cc89345eeeb869b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368888"
---
# <a name="title-element"></a>title 元素


所需**标题**元素提供事件通知消息的标题中显示的文本。

**标题**中定义元素*asyncui*此 URI 处的命名空间： http://schemas.microsoft.com/2003/print/asyncui/v1/request。 （此资源可能不会在某些语言和国家/地区中可用。）

<a name="usage"></a>用法
-----

```xml
<title
  stringID = "xs:string"
  resourceDll = "xs:string"/>
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
<p>一个指定的资源 DLL，其中包含要显示在事件通知消息的标题文本的可选属性。 此 DLL 应是打印机驱动程序的依赖文件和驱动程序资源文件夹 （例如，%systemroot%\system32\spool\drivers\w32x86\3) 中必须存在。</p></td>
</tr>
<tr class="even">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>指定要显示的标题中的事件通知消息的文本的所需的属性。 属性值的资源 DLL 中指定的文本字符串的位置。</p></td>
</tr>
</tbody>
</table>

## <a name="child-elements"></a>子元素


没有子元素。

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
</tbody>
</table>

<a name="remarks"></a>备注
-------

如果该属性**项 resourceDll**未指定，则从 Microsoft 提供的用户接口 DLL，Prnntfy.dll 生成标题文本。

从资源 DLL 加载的正文文本可以包含百分比 （%）将替换为指定的文本字符串的字符[**参数**](parameter.md)子元素。

<a name="examples"></a>示例
--------

下面的代码示例演示如何使用**标题**元素以指示资源 DLL 中的字符串位置 (在此示例中，字符串 Id ="1234")，包含要用于标题的文本。

```cpp
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

[parameter](parameter.md)
