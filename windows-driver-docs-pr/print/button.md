---
title: Button 元素
description: 所需的按钮元素在客户端计算机显示一个消息框中指定的一个按钮的特征。
ms.assetid: 3e210599-9412-4eea-a024-338e39852199
keywords:
- 打印设备的 button 元素
topic_type:
- apiref
api_name:
- button
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8abffb192f94b44696a93db9cb7c8e0e6a794be3
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464307"
---
# <a name="button-element"></a>Button 元素


所需**按钮**元素在客户端计算机显示一个消息框中指定的一个按钮的特征。

**按钮**中定义元素*asyncui*此 URI 处的命名空间： http://schemas.microsoft.com/2003/print/asyncui/v1/request。 （此资源可能不会在某些语言和国家/地区中可用。）

<a name="usage"></a>用法
-----

```xml
<button
  stringID = "xs:string"
  resourceDll = "xs:string"
  buttonID = "xs:string"/>
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
<td><p><strong>buttonID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>必需的属性，指定当用户单击按钮时将返回到的打印机驱动程序的字符串。 此特性可以采用以下值之一：</p>
IDOK 一个按钮具有名称"确定"将显示在消息框中。 当用户单击按钮时，消息框将返回字符串"IDOK"。
IDCANCEL 一个具有名称"取消"按钮将显示在消息框中。 当用户单击按钮时，消息框将返回字符串"IDCANCEL"。</td>
</tr>
<tr class="even">
<td><p><strong>resourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>一个可选属性，指定的资源 DLL，其中包含要在按钮上显示的文本。 此 DLL 应是打印机驱动程序的依赖文件和驱动程序资源文件夹 （例如，%systemroot%\system32\spool\drivers\w32x86\3) 中必须存在。</p></td>
</tr>
<tr class="odd">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>指定要在按钮上显示的文本的所需的属性。 属性值的资源 DLL 中指定的文本字符串的位置。</p></td>
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
<td><p><a href="buttons.md" data-raw-source="[&lt;strong&gt;buttons&lt;/strong&gt;](buttons.md)"><strong>buttons</strong></a></p></td>
<td><p></p>
<p>必需的元素，用于指定一个或多个按钮的显示客户端计算机上的事件中的通知消息框。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

按钮将显示在消息框的底部。

<a name="examples"></a>示例
--------

下面的代码示例演示如何使用**按钮**元素以显示**确定**并**取消**彼此的按钮。

```xml
<?xml version="1.0" ?>
  <asyncPrintUIRequest
    xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/request">
    <v1>
      <requestOpen>
        <messageBoxUI>
          <title stringID="1234" resourceDll="IHV.dll" />
          <body stringID="100" resourceDll="IHV.dll">
            <parameter stringID="5" />
            <parameter stringID="1002" resourceDll="IHV.dll" />
          </body>
          <buttons>
            <button stringID="1" resourceDll="IHV.dll" buttonID="IDOK"/>
            <button stringID="2" resourceDll="IHV.dll" buttonID="IDCANCEL"/>
          </buttons>
        </messageBoxUI>
      </requestOpen>
    </v1>
  </asyncPrintUIRequest>
```

## <a name="see-also"></a>请参阅

[buttons](buttons.md)
