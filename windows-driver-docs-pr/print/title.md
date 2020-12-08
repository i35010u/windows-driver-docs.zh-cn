---
title: title 元素
description: Required title 元素提供在事件通知消息标题中显示的文本。
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
ms.openlocfilehash: fc2535924f0f0bb3d912e07c653582e2837a4af7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806699"
---
# <a name="title-element"></a>title 元素

Required **title** 元素提供在事件通知消息标题中显示的文本。

**Title** 元素在 *asyncui* 命名空间中的此 URI 上定义：

```xml
https://schemas.microsoft.com/2003/print/asyncui/v1/request
```

此资源可能在某些语言和国家/地区不可用。

## <a name="usage"></a>使用情况

```xml
<title
  stringID = "xs:string"
  resourceDll = "xs:string"/>
```

## <a name="attributes"></a>特性

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
<th>类型</th>
<th>必须</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>resourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>一个可选属性，它指定一个资源 DLL，其中包含要在事件通知消息中显示的标题文本。 此 DLL 应是打印机驱动程序的依赖文件，并且必须位于驱动程序资源文件夹中 (例如%SYSTEMROOT%\system32\spool\drivers\w32x86\3) 。</p></td>
</tr>
<tr class="even">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>一个必需的属性，指定要在事件通知消息标题中显示的文本。 属性值指定资源 DLL 中文本字符串的位置。</p></td>
</tr>
</tbody>
</table>

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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="balloonui.md" data-raw-source="[&lt;strong&gt;balloonUI&lt;/strong&gt;](balloonui.md)"><strong>balloonUI</strong></a></p></td>
<td><p></p>
<p>一个可选元素，用于在客户端计算机上显示消息气球。</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>备注

如果未指定属性 **resourceDll** ，则从 Microsoft 提供的用户界面 DLL Prnntfy.dll 中生成标题文本。

从资源 DLL 加载的正文文本可以包含百分比 (% ) 字符，这些字符将替换为 [**参数**](parameter.md) 子元素指定的文本字符串。

## <a name="examples"></a>示例

下面的代码示例演示如何使用 **title** 元素来指示资源 DLL 中的字符串位置 (本例中为 stringID = "1234" ) ，其中包含要用于标题的文本。

```cpp
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

[balloonUI](balloonui.md)

[参数](parameter.md)
