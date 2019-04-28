---
title: asyncPrintUIRequest 元素
description: 所需的 asyncPrintUIRequest 元素描述打印机驱动程序发出的客户端计算机上创建一条消息的请求。
ms.assetid: 992e3c97-b148-4802-be48-3067adb6dd0d
keywords:
- asyncPrintUIRequest 元素打印设备
topic_type:
- apiref
api_name:
- asyncPrintUIRequest
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 023928b2266a5577ed1271ecf61daef6870e1692
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331211"
---
# <a name="asyncprintuirequest-element"></a>asyncPrintUIRequest 元素


所需**asyncPrintUIRequest**元素描述打印机驱动程序发出的客户端计算机上创建一条消息的请求。

**AsyncPrintUIRequest**中定义元素*asyncui*此 URI 处的命名空间： http://schemas.microsoft.com/2003/print/asyncui/v1/request。

<a name="usage"></a>用法
-----

```xml
<asyncPrintUIRequest>
  child elements
</asyncPrintUIRequest>
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
<td><p><a href="requestclose.md" data-raw-source="[&lt;strong&gt;requestClose&lt;/strong&gt;](requestclose.md)"><strong>requestClose</strong></a></p></td>
<td><p></p>
<p>可选元素，它用于关闭客户端计算机上的事件通知消息。</p></td>
</tr>
<tr class="even">
<td><p><a href="requestopen.md" data-raw-source="[&lt;strong&gt;requestOpen&lt;/strong&gt;](requestopen.md)"><strong>requestOpen</strong></a></p></td>
<td><p></p>
<p>一个用于打开客户端计算机上的事件通知消息的元素。</p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素


没有父元素。

<a name="examples"></a>示例
--------

下面的代码示例演示如何使用**asyncPrintUIRequest**元素。

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


[**requestClose**](requestclose.md)

[**requestOpen**](requestopen.md)

 

 




