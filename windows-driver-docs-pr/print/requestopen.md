---
title: requestOpen 元素
description: RequestOpen 元素用于在客户端计算机上打开事件通知消息。
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
ms.openlocfilehash: 95525612525dafca7e74f4bbe7048ede388c1e95
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881905"
---
# <a name="requestopen-element"></a>requestOpen 元素

**RequestOpen**元素用于在客户端计算机上打开事件通知消息。

**RequestOpen**元素在*asyncui*命名空间中的此 URI 上定义： [http://schemas.microsoft.com/2003/print/asyncui/v1/request](https://schemas.microsoft.com/2003/print/asyncui/v1/request)。 （此资源可能在某些语言和国家/地区不可用。）

## <a name="usage"></a>Usage

```xml
<requestOpen>
  child elements
</requestOpen>
```

## <a name="attributes"></a>属性

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
<p>一个可选元素，用于在客户端计算机上显示消息气球。</p></td>
</tr>
<tr class="even">
<td><p><a href="customui.md" data-raw-source="[&lt;strong&gt;customUI&lt;/strong&gt;](customui.md)"><strong>customUI</strong></a></p></td>
<td><p></p>
<p>一个可选元素，该元素指定要在客户端计算机上显示的自定义用户界面。</p></td>
</tr>
<tr class="odd">
<td><p><a href="messageboxui.md" data-raw-source="[&lt;strong&gt;messageBoxUI&lt;/strong&gt;](messageboxui.md)"><strong>messageBoxUI</strong></a></p></td>
<td><p></p>
<p>一个可选元素，用于在客户端计算机上显示消息框。</p></td>
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
<p>一个必需的元素，描述打印机驱动程序发出的用于在客户端计算机上创建消息的请求。</p></td>
</tr>
</tbody>
</table>

## <a name="examples"></a>示例

下面的代码示例将打开一个事件通知消息。

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

## <a name="see-also"></a>另请参阅

[asyncPrintUIRequest](asyncprintuirequest.md)

[balloonUI](balloonui.md)

[customUI](customui.md)

[messageBoxUI](messageboxui.md)

[requestClose](requestclose.md)
