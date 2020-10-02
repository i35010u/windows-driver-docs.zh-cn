---
title: asyncPrintUIRequest 元素
description: 必需的 asyncPrintUIRequest 元素描述由打印机驱动程序发出的请求，以在客户端计算机上创建消息。
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
ms.openlocfilehash: aac1479b453a1795d5188c74abe279f6e8a3d7fe
ms.sourcegitcommit: b3e38d06762246c77cedd8e82d740ebea104c538
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91662479"
---
# <a name="asyncprintuirequest-element"></a>asyncPrintUIRequest 元素

必需的 **asyncPrintUIRequest** 元素描述由打印机驱动程序发出的请求，以在客户端计算机上创建消息。

**AsyncPrintUIRequest**元素在*asyncui*命名空间中的此 URI 处定义：

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
<th>说明</th>
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
