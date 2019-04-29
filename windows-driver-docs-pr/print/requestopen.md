---
title: requestOpen 元素
description: RequestOpen 元素用于打开客户端计算机上的事件通知消息。
ms.assetid: c1797295-9aca-4986-bd9d-482bb7049942
keywords:
- requestOpen 元素打印设备
topic_type:
- apiref
api_name:
- requestOpen
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2fd86abbcfd958661da4b3e3ced547837ffa93b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382574"
---
# <a name="requestopen-element"></a>requestOpen 元素


**RequestOpen**元素用于打开客户端计算机上的事件通知消息。

**RequestOpen**中定义元素*asyncui*此 URI 处的命名空间： http://schemas.microsoft.com/2003/print/asyncui/v1/request。 （此资源可能不会在某些语言和国家/地区中可用。）

<a name="usage"></a>用法
-----

```xml
<requestOpen>
  child elements
</requestOpen>
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
<td><p><a href="balloonui.md" data-raw-source="[&lt;strong&gt;balloonUI&lt;/strong&gt;](balloonui.md)"><strong>balloonUI</strong></a></p></td>
<td><p></p>
<p>一个用于客户端计算机上显示消息气泡的可选元素。</p></td>
</tr>
<tr class="even">
<td><p><a href="customui.md" data-raw-source="[&lt;strong&gt;customUI&lt;/strong&gt;](customui.md)"><strong>customUI</strong></a></p></td>
<td><p></p>
<p>一个指定要在客户端计算机上显示的自定义用户界面的可选元素。</p></td>
</tr>
<tr class="odd">
<td><p><a href="messageboxui.md" data-raw-source="[&lt;strong&gt;messageBoxUI&lt;/strong&gt;](messageboxui.md)"><strong>messageBoxUI</strong></a></p></td>
<td><p></p>
<p>可选元素，它用于在客户端计算机上显示一个消息框。</p></td>
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
<td><p><a href="asyncprintuirequest.md" data-raw-source="[&lt;strong&gt;asyncPrintUIRequest&lt;/strong&gt;](asyncprintuirequest.md)"><strong>asyncPrintUIRequest</strong></a></p></td>
<td><p></p>
<p>描述打印机驱动程序发出的客户端计算机上创建一条消息的请求所必需的元素。</p></td>
</tr>
</tbody>
</table>

<a name="examples"></a>示例
--------

下面的代码示例将打开的事件通知消息。

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

[asyncPrintUIRequest](asyncprintuirequest.md)

[balloonUI](balloonui.md)

[customUI](customui.md)

[messageBoxUI](messageboxui.md)

[requestClose](requestclose.md)
