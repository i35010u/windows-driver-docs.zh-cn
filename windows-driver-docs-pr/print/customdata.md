---
title: customData 元素
description: 可选的 customData 元素为此异步通知 XML 架构指定自定义数据源。
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
ms.openlocfilehash: 58f6b7a57c60e8b243adac47833b5a05b8758f08
ms.sourcegitcommit: b3e38d06762246c77cedd8e82d740ebea104c538
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91662383"
---
# <a name="customdata-element"></a>customData 元素

可选的 **customData** 元素为此异步通知 XML 架构指定自定义数据源。

**CustomData**元素在*asyncui*命名空间中的此 URI 处定义：

```xml
https://schemas.microsoft.com/2003/print/asyncui/v1/request
```

此资源可能在某些语言和国家/地区不可用。

## <a name="usage"></a>使用情况

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
<th>属性</th>
<th>类型</th>
<th>必需</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>bidi</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>一个必需的属性，该属性指定打印机驱动程序和事件通知消息之间的通信类型。 如果该值为 <strong>true</strong>，则通信是双向的，并且资源 DLL 中的驱动程序函数必须返回一个字符串。 如果该值为 <strong>false</strong>，则通信是单向的，从打印机驱动程序到事件通知消息。 有关详细信息，请参阅下面的示例和备注部分。</p></td>
</tr>
<tr class="even">
<td><p><strong>.dll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>指定包含自定义数据源的资源 DLL 的必需特性。 此 DLL 应是打印机驱动程序的依赖文件，并且必须位于驱动程序资源文件夹中 (例如%SYSTEMROOT%\system32\spool\drivers\w32x86\3) 。</p></td>
</tr>
<tr class="odd">
<td><p><strong>入口</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>一个必需的属性，该属性指定资源 DLL 中的数据源入口点。</p></td>
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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>任何内容</strong></p></td>
<td><p></p>
<p>根据自定义数据架构指定任何子元素。 有关详细信息，请参阅以下示例部分。</p></td>
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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="requestopen.md" data-raw-source="[&lt;strong&gt;requestOpen&lt;/strong&gt;](requestopen.md)"><strong>requestOpen</strong></a></p></td>
<td><p></p>
<p>用于在客户端计算机上打开事件通知消息的元素。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

捕获的自定义数据必须作为 **CDATA** 类型提供。

<a name="examples"></a>示例
--------

下面的代码示例演示如何使用 **customData** 元素获取自定义数据。

```xml
<?xml version="1.0"?>
  <asyncPrintUIRequest xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/request"
      xmlns:myco="https://www.myprintercompany.com">
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
