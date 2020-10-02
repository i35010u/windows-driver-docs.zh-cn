---
title: requestClose 元素
description: 可选的 requestClose 元素用于在客户端计算机上关闭事件通知消息。
ms.assetid: b2f21ab2-9205-483c-9f56-1c877edb7da2
keywords:
- requestClose 元素打印设备
topic_type:
- apiref
api_name:
- requestClose
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 012a86dcc2f90c90dbf1b84f29030530f93fea9e
ms.sourcegitcommit: b3e38d06762246c77cedd8e82d740ebea104c538
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91662431"
---
# <a name="requestclose-element"></a>requestClose 元素

可选的 **requestClose** 元素用于在客户端计算机上关闭事件通知消息。

**RequestClose**元素在*asyncui*命名空间中的此 URI 处定义：

```xml
https://schemas.microsoft.com/2003/print/asyncui/v1/request
```

此资源可能在某些语言和国家/地区不可用。

## <a name="usage"></a>使用情况

```xml
<requestClose/>
```

## <a name="attributes"></a>特性

没有特性。

## <a name="child-elements"></a>子元素

没有任何子元素。

## <a name="parent-elements"></a>父元素

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
<td><p><a href="asyncprintuirequest.md" data-raw-source="[&lt;strong&gt;asyncPrintUIRequest&lt;/strong&gt;](asyncprintuirequest.md)"><strong>asyncPrintUIRequest</strong></a></p></td>
<td><p></p>
<p>一个必需的元素，描述打印机驱动程序发出的用于在客户端计算机上创建消息的请求。</p></td>
</tr>
</tbody>
</table>

## <a name="examples"></a>示例

下面的代码示例演示了如何在为 **"确定"** 按钮捕获消息框后关闭事件通知。

```cpp
<?xml version="1.0" ?>
   <asyncPrintUIResponse
    xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/response">
    <v1>
      <requestClose>
        <messageBoxUI>
          <buttonID>IDOK</buttonID>
        </messageBoxUI>
      </requestClose>
    </v1>
  </asyncPrintUIResponse>
```

## <a name="see-also"></a>请参阅

[asyncPrintUIRequest](asyncprintuirequest.md)

[requestOpen](requestopen.md)
