---
title: parameter 元素
description: 可选参数元素指定替换为事件通知消息的文本中的百分比 （） 字符的文本字符串。
ms.assetid: 6a43af7d-da00-4038-b1a8-a076d07c4c1a
keywords:
- parameter 元素打印设备
topic_type:
- apiref
api_name:
- parameter
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 820b1985308399f83af8cb2b23b594e5763aebe2
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464260"
---
# <a name="parameter-element"></a>parameter 元素


可选**参数**元素指定的文本字符串替换为百分比 （%）事件通知消息的文本中的字符。

**参数**中定义元素*asyncui*此 URI 处的命名空间： http://schemas.microsoft.com/2003/print/asyncui/v1/request。 （此资源可能不会在某些语言和国家/地区中可用。）

<a name="usage"></a>用法
-----

```xml
<parameter
  stringID = "xs:string"
  resourceDll = "xs:string"
  type = "xs:string"/>
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
<p>一个可选属性，指定的资源 DLL，其中包含要显示在事件通知消息的文本。 此 DLL 应是打印机驱动程序的依赖文件和驱动程序资源文件夹 （例如，%systemroot%\system32\spool\drivers\w32x86\3) 中必须存在。</p></td>
</tr>
<tr class="even">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>指定要在百分比 （%） 的位置显示的文本的所需的属性事件通知消息的文本中的字符。 属性值的资源 DLL 中指定的文本字符串的位置。</p></td>
</tr>
<tr class="odd">
<td><p><strong>type</strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>一个可选属性，指定文档的打印机的名称。 此特性可以采用正在打印的文档的以下值： DocumentThe 名称之一。PrinterNameThe 名称如下所示的打印机和传真打印机的控制面板中，例如，"Fabrikam 5000 上 \printserver"中的文件夹或"楼上的卧室中的打印机"。</p></td>
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
<td><p><a href="body.md" data-raw-source="[&lt;strong&gt;body&lt;/strong&gt;](body.md)"><strong>body</strong></a></p></td>
<td><p></p>
<p>提供的文本的所需的元素显示在事件通知消息。 此文本应提供用户有关打印机事件的特定详细信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="title.md" data-raw-source="[&lt;strong&gt;title&lt;/strong&gt;](title.md)"><strong>title</strong></a></p></td>
<td><p></p>
<p>所需的标题元素提供事件通知消息的标题中显示的文本。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

加载资源 DLL 中的文本可以包含百分比 （%）将替换为指定的文本字符串的字符**参数**元素。

<a name="examples"></a>示例
--------

下面的代码示例演示如何**参数**元素可用于生成完整的事件通知消息。

在此示例中， **stringid 为**值指定以下内容：

-   驱动程序资源 DLL 中的用户界面字符串 100 为"打印机 %1 墨水; 用完请打开 %2 并更换墨盒。"
-   Microsoft 提供的用户界面 DLL 中的用户界面字符串 5 为"黄色"。
-   驱动程序资源 DLL 中的用户界面字符串 1002年是"端访问门 B"。

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

使用前面的 XML 代码，以下正文文本 (字符串 Id ="100") 将显示在事件通知消息："打印机是黄色墨水; 用完请打开门 B 端访问并更换墨盒。"

## <a name="see-also"></a>请参阅

[body](body.md)

[title](title.md)
