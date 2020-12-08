---
title: 参数元素
description: 可选的 parameter 元素指定一个文本字符串，该字符串将替换为事件通知消息文本中 ( ) 字符的百分比。
keywords:
- 参数元素打印设备
topic_type:
- apiref
api_name:
- parameter
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad5b9be6607fc269432762921a5e046ad37cd15f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807633"
---
# <a name="parameter-element"></a>参数元素

可选的 **parameter** 元素指定一个文本字符串，该字符串用来替换事件通知消息文本中 (% ) 字符的百分比。

**Parameter** 元素在 *asyncui* 命名空间中的此 URI 上定义：

```xml
https://schemas.microsoft.com/2003/print/asyncui/v1/request
```

此资源可能在某些语言和国家/地区不可用。

## <a name="usage"></a>使用情况

```xml
<parameter
  stringID = "xs:string"
  resourceDll = "xs:string"
  type = "xs:string"/>
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
<p>一个可选属性，该属性指定包含要在事件通知消息中显示的文本的资源 DLL。 此 DLL 应是打印机驱动程序的依赖文件，并且必须位于驱动程序资源文件夹中 (例如%SYSTEMROOT%\system32\spool\drivers\w32x86\3) 。</p></td>
</tr>
<tr class="even">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>一个必需的属性，该属性指定在事件通知消息的文本中 (% ) 字符的百分比位置要显示的文本。 属性值指定资源 DLL 中文本字符串的位置。</p></td>
</tr>
<tr class="odd">
<td><p>type</p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>一个可选属性，用于指定打印机或文档的名称。 此属性可采用以下值之一： DocumentThe 要打印的文档的名称。PrinterNameThe 打印机的名称，如 "控制面板" 的 "打印机和传真" 文件夹中所列，例如，"\printserver 上的 Fabrikam 5000" 或 "Printer in 楼上卧室窗户外面"。</p></td>
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
<td><p><a href="body.md" data-raw-source="[&lt;strong&gt;body&lt;/strong&gt;](body.md)"><strong>body</strong></a></p></td>
<td><p></p>
<p>一个必需的元素，它提供在事件通知消息中显示的文本。 此文本应提供有关打印机事件的用户特定详细信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="title.md" data-raw-source="[&lt;strong&gt;title&lt;/strong&gt;](title.md)"><strong>title</strong></a></p></td>
<td><p></p>
<p>Required title 元素提供在事件通知消息标题中显示的文本。</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>备注

从资源 DLL 加载的文本可以包含百分比 (% ) 字符，这些字符将替换为 **parameter** 元素所指定的文本字符串。

## <a name="examples"></a>示例

下面的代码示例演示如何使用 **parameter** 元素生成完整的事件通知消息。

在此示例中， **stringID** 值指定了以下内容：

- 驱动程序资源 DLL 中的用户界面字符串100为 "打印机超出了 %1 墨迹;请打开 %2 并替换墨盒。

- Microsoft 提供的用户界面 DLL 中的用户界面字符串5为 "黄色"。

- 驱动程序资源 DLL 中的用户界面字符串1002是 "端访问门 B"。

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

对于前面的 XML 代码，以下正文文本 (stringID = "100" ) 出现在事件通知消息中： "打印机已超出黄色墨迹;请打开侧访问门 B 并替换墨盒。

## <a name="see-also"></a>请参阅

[body](body.md)

[title](title.md)
