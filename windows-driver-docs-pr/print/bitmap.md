---
title: Bitmap 元素
description: 可选位图元素用于在消息框中的正文文本的左侧显示位图图像。
ms.assetid: 6dd1a82f-7a9e-4ed6-9d0d-76e025331d2c
keywords:
- bitmap 元素打印设备
topic_type:
- apiref
api_name:
- bitmap
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c46cf501af5e680636000845abbfed33c5e8d92d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556019"
---
# <a name="bitmap-element"></a>Bitmap 元素


可选**位图**元素用于在消息框中的正文文本的左侧显示位图图像。

**位图**中定义元素*asyncui*此 URI 处的命名空间： http://schemas.microsoft.com/2003/print/asyncui/v1/request。 （此资源可能不会在某些语言和国家/地区中可用。）

<a name="usage"></a>用法
-----

```xml
<bitmap
  bitmapID = "xs:string"
  resourceDll = "xs:string"/>
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
<td><p><strong>bitmapID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>指定在消息框中显示的位图图像的所需的属性。 属性值的资源 DLL 中指定的映像的位置。 位图图像可以是任何大小或格式;消息框将调整大小以容纳它。</p></td>
</tr>
<tr class="even">
<td><p><strong>resourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>一个指定的资源 DLL，其中包含要在消息框中显示的位图图像的可选属性。 此 DLL 应是打印机驱动程序的依赖文件和驱动程序资源文件夹 （例如，%systemroot%\system32\spool\drivers\w32x86\3) 中必须存在。</p></td>
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
<td><p><a href="messageboxui.md" data-raw-source="[&lt;strong&gt;messageBoxUI&lt;/strong&gt;](messageboxui.md)"><strong>messageBoxUI</strong></a></p></td>
<td><p></p>
<p>可选元素，它用于在客户端计算机上显示一个消息框。</p></td>
</tr>
</tbody>
</table>

<a name="examples"></a>示例
--------

下面的代码示例演示如何使用**位图**元素。

```xml
<?xml version="1.0" ?>
   <asyncPrintUIRequest xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/request">
    <v1>
      <requestOpen>
        <messageBoxUI>
          <title stringID="1234" resourceDll="IHV.dll" />
          <bitmap bitmapID="100" resourceDll="IHV.dll" />
          <body stringID="100" resourceDll="IHV.dll">
            <parameter stringID="5" />
            <parameter stringID="1002" resourceDll="IHV.dll" />
          </body>
        </messageBoxUI>
      </requestOpen>
    </v1>
  </asyncPrintUIRequest>
```

## <a name="see-also"></a>另请参阅

[**messageBoxUI**](messageboxui.md)
