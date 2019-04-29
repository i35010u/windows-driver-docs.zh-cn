---
title: customData 元素
description: 可选 customData 元素指定此异步通知 XML 架构的自定义数据源。
ms.assetid: 5e14a627-72c0-440d-b616-6963c3d69d2b
keywords:
- customData 元素打印设备
topic_type:
- apiref
api_name:
- customData
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea25442cd8a1eabed1831b904a72b2526b7c90b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365553"
---
# <a name="customdata-element"></a>customData 元素


可选**customData**元素指定此异步通知 XML 架构的自定义数据源。

**CustomData**中定义元素*asyncui*此 URI 处的命名空间： http://schemas.microsoft.com/2003/print/asyncui/v1/request。 （此资源可能不会在某些语言和国家/地区中可用。）

<a name="usage"></a>用法
-----

```xml
<customData
  dll = "xs:string"
  entryPoint = "xs:string"
  bidi = "xs:string">
  child elements
</customData>
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
<td><p><strong>bidi</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>指定的打印机驱动程序和事件通知消息之间的通信类型的必需的属性。 如果值为<strong>，则返回 true</strong>，通信是双向的资源 DLL 中的驱动程序函数必须返回一个字符串。 如果值为<strong>false</strong>，通信为单向，从与事件通知消息的打印机驱动程序。 有关详细信息，请参阅下面的示例和备注部分。</p></td>
</tr>
<tr class="even">
<td><p><strong>dll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>指定资源 DLL，其中包含自定义数据源的必需的属性。 此 DLL 应是打印机驱动程序的依赖文件和驱动程序资源文件夹 （例如，%systemroot%\system32\spool\drivers\w32x86\3) 中必须存在。</p></td>
</tr>
<tr class="odd">
<td><p><strong>entryPoint</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>资源 DLL 中指定的数据源的入口点的所需的属性。</p></td>
</tr>
</tbody>
</table>

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
<td><p><strong>任何内容</strong></p></td>
<td><p></p>
<p>指定根据自定义数据架构的任何子元素。 有关详细信息，请参阅下面的示例部分。</p></td>
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
<td><p><a href="requestopen.md" data-raw-source="[&lt;strong&gt;requestOpen&lt;/strong&gt;](requestopen.md)"><strong>requestOpen</strong></a></p></td>
<td><p></p>
<p>一个用于打开客户端计算机上的事件通知消息的元素。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

在捕获自定义数据必须提供作为**CDATA**类型。

<a name="examples"></a>示例
--------

下面的代码示例演示如何使用**customData**元素能够获取自定义数据。

```xml
<?xml version="1.0"?>
  <asyncPrintUIRequest xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/request"
      xmlns:myco="http://www.myprintercompany.com">
    <requestOpen>
      <customData dll="abc.dll" entrypoint="IHVFunction" bidi="true">
        <IHV:anyXMLData />
          CDATA
      </customData>
    </requestOpen>
</asyncPrintUIRequest>
```

## <a name="see-also"></a>请参阅

[requestOpen](requestopen.md)
