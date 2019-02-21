---
title: balloonUI 元素
description: 可选 balloonUI 元素用于在客户端计算机上显示消息气泡。
ms.assetid: 8db15dcb-26ed-429e-ad4c-e5dc59f9bbca
keywords:
- balloonUI 元素打印设备
topic_type:
- apiref
api_name:
- balloonUI
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: db9fa4cc0554f0d6569eb9c8b35cfa95a8964db1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542536"
---
# <a name="balloonui-element"></a>balloonUI 元素


可选**balloonUI**元素用于在客户端计算机上显示消息气泡。

**BalloonUI**中定义元素*asyncui*此 URI 处的命名空间： http://schemas.microsoft.com/2003/print/asyncui/v1/request。 （此资源可能不会在某些语言和国家/地区中可用。）

<a name="usage"></a>用法
-----

```xml
<balloonUI
  iconID = "xs:string"
  resourceDll = "xs:string">
  child elements
</balloonUI>
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
<td><p><strong>iconID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>一个可选属性，指定打印机图标以显示在事件通知消息。 属性值指定的资源 DLL 中的图标的位置。 图标必须是 32 x 32 像素的大小，任何颜色深度。</p></td>
</tr>
<tr class="even">
<td><p><strong>resourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>一个可选属性，指定的资源 DLL，其中包含要显示在事件通知消息的打印机图标。 此 DLL 应是打印机驱动程序的依赖文件和驱动程序资源文件夹 （例如，%systemroot%\system32\spool\drivers\w32x86\3) 中必须存在。</p></td>
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
<td><p><a href="body.md" data-raw-source="[&lt;strong&gt;body&lt;/strong&gt;](body.md)"><strong>body</strong></a></p></td>
<td><p></p>
<p>提供的文本的所需的元素显示在事件通知消息。 此文本应提供用户有关打印机事件的特定详细信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="title.md" data-raw-source="[&lt;strong&gt;title&lt;/strong&gt;](title.md)"><strong>title</strong></a></p></td>
<td><p></p>
<p>提供事件通知消息的标题中显示的文本所必需的元素。</p></td>
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

如果特性**iconID**并**项 resourceDll**未指定，通用打印机图标将显示在气球消息。 若要显示自定义打印机图标，指定这两个属性的值。

<a name="examples"></a>示例
--------

下面的代码示例演示如何使用交互式气球将传递**CDATA**类型到 DLL 的数据。

```xml
<?xml version="1.0" ?> 
  <asyncPrintUIRequest xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/request">
    <v1>
      <requestOpen>
        <balloonUI iconID="1" resourceDll="IHV.dll">
          <title stringID="1234" resourceDll="IHV.dll" />
          <body stringID="100" resourceDll="IHV.dll">
            <parameter stringID="<5>" />
            <parameter stringID="1002" resourceDll="IHV.dll" />
          </body>
          <action dll="adc.dll" entrypoint="def" />
            IHV Data to pass into dll
            MUST BE CDATA
          </action>
        </balloonUI>
      </requestOpen>
    </v1>
  </asyncPrintUIRequest>
```

## <a name="see-also"></a>另请参阅


[**action**](action.md)

[**body**](body.md)

[**requestOpen**](requestopen.md)

[**title**](title.md)

 

 




