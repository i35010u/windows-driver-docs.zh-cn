---
title: asyncPrintUIRequest 元素
description: 必需的 asyncPrintUIRequest 元素描述由打印机驱动程序发出的请求，以在客户端计算机上创建消息。
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
ms.openlocfilehash: 7a7c2a89125a46331f9549d2f0c16a4abd608982
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836127"
---
# <a name="asyncprintuirequest-element"></a>asyncPrintUIRequest 元素

必需的 **asyncPrintUIRequest** 元素描述由打印机驱动程序发出的请求，以在客户端计算机上创建消息。

**AsyncPrintUIRequest** 元素在 *asyncui* 命名空间中的此 URI 处定义：

```xml
https://schemas.microsoft.com/2003/print/asyncui/v1/request
```

此资源可能在某些语言和国家/地区不可用。

## <a name="usage"></a>使用情况

```xml
<asyncPrintUIRequest>
  child elements
</asyncPrintUIRequest>
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
<td><p><a href="requestclose.md" data-raw-source="[&lt;strong&gt;requestClose&lt;/strong&gt;](requestclose.md)"><strong>requestClose</strong></a></p></td>
<td><p></p>
<p>用于在客户端计算机上关闭事件通知消息的可选元素。</p></td>
</tr>
<tr class="even">
<td><p><a href="requestopen.md" data-raw-source="[&lt;strong&gt;requestOpen&lt;/strong&gt;](requestopen.md)"><strong>requestOpen</strong></a></p></td>
<td><p></p>
<p>用于在客户端计算机上打开事件通知消息的元素。</p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>父元素

没有父元素。

## <a name="examples"></a>示例

下面的代码示例演示如何使用 **asyncPrintUIRequest** 元素。

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

## <a name="see-also"></a>请参阅

[**requestClose**](requestclose.md)

[**requestOpen**](requestopen.md)
