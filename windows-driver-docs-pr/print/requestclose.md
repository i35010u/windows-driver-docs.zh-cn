---
title: requestClose 元素
description: 可选 requestClose 元素用于关闭客户端计算机上的事件通知消息。
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
ms.openlocfilehash: da1ed220d080383b7edcafcab9dd2dea67e9710d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524632"
---
# <a name="requestclose-element"></a>requestClose 元素


可选**requestClose**元素用于关闭客户端计算机上的事件通知消息。

**RequestClose**中定义元素*asyncui*此 URI 处的命名空间： http://schemas.microsoft.com/2003/print/asyncui/v1/request。 （此资源可能不会在某些语言和国家/地区中可用。）

<a name="usage"></a>用法
-----

```xml
<requestClose/>
```

<a name="attributes"></a>属性
----------

没有特性。

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
<td><p><a href="asyncprintuirequest.md" data-raw-source="[&lt;strong&gt;asyncPrintUIRequest&lt;/strong&gt;](asyncprintuirequest.md)"><strong>asyncPrintUIRequest</strong></a></p></td>
<td><p></p>
<p>描述打印机驱动程序发出的客户端计算机上创建一条消息的请求所必需的元素。</p></td>
</tr>
</tbody>
</table>

<a name="examples"></a>示例
--------

下面的代码示例演示如何为捕获的消息框上的按钮单击后关闭的事件通知**确定**按钮。

```cpp
<?xml version="1.0" ?>
   <asyncPrintUIResponse
    xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/response">
    <v1>
      <requestClose>
        <messageBoxUI>
          <buttonID>IDOK</buttonID>
        </messageBoxUI>
      </requestClose>
    </v1>
  </asyncPrintUIResponse>
```

## <a name="see-also"></a>另请参阅

[asyncPrintUIRequest](asyncprintuirequest.md)

[requestOpen](requestopen.md)
