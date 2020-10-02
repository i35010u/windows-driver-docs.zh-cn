---
title: customUI 元素
description: 可选的 customUI 元素指定要在客户端计算机上显示的自定义用户界面。
ms.assetid: 4408dcf2-0928-4ecb-97eb-0027eceef457
keywords:
- customUI 元素打印设备
topic_type:
- apiref
api_name:
- customUI
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f558fd60d1fea192523532e085e8b17900d1a01c
ms.sourcegitcommit: b3e38d06762246c77cedd8e82d740ebea104c538
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91662410"
---
# <a name="customui-element"></a>customUI 元素

可选的 **customUI** 元素指定要在客户端计算机上显示的自定义用户界面。

**CustomUI**元素在*asyncui*命名空间中的此 URI 处定义：

```xml
https://schemas.microsoft.com/2003/print/asyncui/v1/request
```

此资源可能在某些语言和国家/地区不可用。

## <a name="usage"></a>使用情况

```xml
<customUI
  dll = "xs:string"
  entrypoint = "xs:string"
  bidi = "xs:string">
  child elements
</customUI>
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
<p>一个必需的属性，该属性指定打印机驱动程序和事件通知消息之间的通信类型。 如果该值为 <strong>true</strong>，则通信是双向的，并且资源 DLL 中的驱动程序函数必须返回字符串;请参阅 "示例" 部分。 如果该值为 <strong>false</strong>，则通信是单向的，从打印机驱动程序到事件通知消息。</p></td>
</tr>
<tr class="even">
<td><p><strong>.dll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>一个必需的属性，指定包含自定义用户界面显示功能的资源 DLL。 此 DLL 应是打印机驱动程序的依赖文件，并且必须位于驱动程序资源文件夹中 (例如%SYSTEMROOT%\system32\spool\drivers\w32x86\3) 。</p></td>
</tr>
<tr class="odd">
<td><p><strong>入口</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>一个必需的属性，它指定要在资源 DLL 中调用的函数。</p></td>
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
<p>根据自定义用户界面架构指定任何子元素。 请参见“示例”一节。</p></td>
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

由于在下面的示例中，**双向**特性设置为**true** ，因此将调用*Abc.dll* DLL 中的**IHVFunction**入口点函数。 **IHVfunction** 返回 **CDATA** 类型数据。

<a name="examples"></a>示例
--------

下面的代码示例演示如何使用 **customUI** 元素调用并显示客户端计算机上的自定义用户界面。

```cpp
<?xml version="1.0"?>
  <asyncPrintUIRequest xmlns="https://schemas.microsoft.com/2003/print/asyncui/1.0"
      xmlns:myco="https://www.myprintercompany.com">
    <requestOpen>
      <customUI dll="abc.dll" entrypoint="IHVFunction" bidi="true">
        <IHV:anyXMLData />
          CDATA
      </customUI>
    </requestOpen>
  </asyncPrintUIRequest>
```

## <a name="see-also"></a>请参阅


[**requestOpen**](requestopen.md)

 

 




