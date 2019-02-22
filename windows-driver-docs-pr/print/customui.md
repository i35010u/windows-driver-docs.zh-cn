---
title: customUI 元素
description: 可选 customUI 元素指定要在客户端计算机上显示的自定义用户界面。
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
ms.openlocfilehash: dca4d106772e8e5e97631889d3b6b9b465e0c25a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544500"
---
# <a name="customui-element"></a>customUI 元素


可选**customUI**元素指定要在客户端计算机上显示的自定义用户界面。

**CustomUI**中定义元素*asyncui*此 URI 处的命名空间： http://schemas.microsoft.com/2003/print/asyncui/v1/request。 （此资源可能不会在某些语言和国家/地区中可用。）

<a name="usage"></a>用法
-----

```xml
<customUI
  dll = "xs:string"
  entrypoint = "xs:string"
  bidi = "xs:string">
  child elements
</customUI>
```

<a name="attributes"></a>属性
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
<p>指定的打印机驱动程序和事件通知消息之间的通信类型的必需的属性。 如果值为<strong>，则返回 true</strong>，通信是双向的资源 DLL 中的驱动程序函数必须返回一个字符串; 请参阅示例部分。 如果值为<strong>false</strong>，通信为单向，从与事件通知消息的打印机驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><strong>dll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>指定资源 DLL，其中包含自定义用户界面显示函数的必需的属性。 此 DLL 应是打印机驱动程序的依赖文件和驱动程序资源文件夹 （例如，%systemroot%\system32\spool\drivers\w32x86\3) 中必须存在。</p></td>
</tr>
<tr class="odd">
<td><p><strong>entrypoint</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>资源 DLL 中指定要调用的函数的必需的属性。</p></td>
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
<p>指定根据自定义用户接口架构的任何子元素。 请参阅示例部分。</p></td>
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

因为**bidi**属性设置为**true**在以下示例中， **IHVFunction**中的入口点函数*Abc.dll* DLL将调用。 **IHVfunction**将返回**CDATA**类型数据。

<a name="examples"></a>示例
--------

下面的代码示例演示如何使用**customUI**要调用并显示客户端计算机上的自定义用户界面元素。

```cpp
<?xml version="1.0"?>
  <asyncPrintUIRequest xmlns="http://schemas.microsoft.com/2003/print/asyncui/1.0"
      xmlns:myco="http://www.myprintercompany.com">
    <requestOpen>
      <customUI dll="abc.dll" entrypoint="IHVFunction" bidi="true">
        <IHV:anyXMLData />
          CDATA
      </customUI>
    </requestOpen>
  </asyncPrintUIRequest>
```

## <a name="see-also"></a>另请参阅


[**requestOpen**](requestopen.md)

 

 




