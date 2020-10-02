---
title: button 元素
description: "\"必需\" 按钮元素指定客户端计算机上显示的消息框中按钮的特征。"
ms.assetid: 3e210599-9412-4eea-a024-338e39852199
keywords:
- button 元素打印设备
topic_type:
- apiref
api_name:
- button
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 612edc906fccdfad929efa59be5471af45a3e994
ms.sourcegitcommit: b3e38d06762246c77cedd8e82d740ebea104c538
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91662331"
---
# <a name="button-element"></a>button 元素

"必需" **按钮** 元素指定客户端计算机上显示的消息框中按钮的特征。

在*asyncui*命名空间中，此 URI 处定义了**button**元素：

```xml
https://schemas.microsoft.com/2003/print/asyncui/v1/request
```

此资源可能在某些语言和国家/地区不可用。

## <a name="usage"></a>使用情况

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
<th>属性</th>
<th>类型</th>
<th>必需</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>buttonID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>一个必需的属性，该属性指定当用户单击按钮时将返回到打印机驱动程序的字符串。 此属性可以采用下列值之一：</p>
IDOK 将在消息框中显示一个名为 "确定" 的按钮。 当用户单击该按钮时，消息框返回字符串 "IDOK"。
IDCANCEL 将在消息框中显示一个名为 "CANCEL" 的按钮。 当用户单击该按钮时，消息框返回字符串 "IDCANCEL"。</td>
</tr>
<tr class="even">
<td><p><strong>resourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>一个可选属性，该属性指定包含要在按钮上显示的文本的资源 DLL。 此 DLL 应是打印机驱动程序的依赖文件，并且必须位于驱动程序资源文件夹中 (例如%SYSTEMROOT%\system32\spool\drivers\w32x86\3) 。</p></td>
</tr>
<tr class="odd">
<td><p><strong>stringID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>一个必需的属性，指定要在按钮上显示的文本。 属性值指定资源 DLL 中文本字符串的位置。</p></td>
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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="buttons.md" data-raw-source="[&lt;strong&gt;buttons&lt;/strong&gt;](buttons.md)"><strong>buttons</strong></a></p></td>
<td><p></p>
<p>一个必需的元素，该元素指定客户端计算机上的事件通知消息框中显示的一个或多个按钮。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

按钮将显示在消息框的底部。

<a name="examples"></a>示例
--------

下面的代码示例演示如何使用 **button** 元素显示彼此相邻的 **"确定" 和 "** **取消** " 按钮。

```xml
<?xml version="1.0" ?>
  <asyncPrintUIRequest
    xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/request">
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
