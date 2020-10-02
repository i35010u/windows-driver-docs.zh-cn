---
title: bitmap 元素
description: 可选的 bitmap 元素用于在消息框中显示正文文本左侧的位图图像。
ms.assetid: 6dd1a82f-7a9e-4ed6-9d0d-76e025331d2c
keywords:
- 位图元素打印设备
topic_type:
- apiref
api_name:
- bitmap
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4bb43d3d1cec0df6dfabd7930aad33a4e5fb1a0
ms.sourcegitcommit: b3e38d06762246c77cedd8e82d740ebea104c538
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91662453"
---
# <a name="bitmap-element"></a>bitmap 元素

可选的 **bitmap** 元素用于在消息框中显示正文文本左侧的位图图像。

**Bitmap**元素在*asyncui*命名空间中的此 URI 上定义：

```xml
https://schemas.microsoft.com/2003/print/asyncui/v1/request
```

此资源可能在某些语言和国家/地区不可用。

## <a name="usage"></a>使用情况

```xml
<bitmap
  bitmapID = "xs:string"
  resourceDll = "xs:string"/>
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
<th>必需</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>bitmapID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>一个必需的属性，该属性指定要在消息框中显示的位图图像。 属性值指定映像在资源 DLL 中的位置。 位图图像可以是任意大小，也可以是格式。消息框将调整大小以容纳该消息框。</p></td>
</tr>
<tr class="even">
<td><p><strong>resourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>否</p></td>
<td><p></p>
<p>一个可选属性，该属性指定包含要在消息框中显示的位图图像的资源 DLL。 此 DLL 应是打印机驱动程序的依赖文件，并且必须位于驱动程序资源文件夹中 (例如%SYSTEMROOT%\system32\spool\drivers\w32x86\3) 。</p></td>
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
<td><p><a href="messageboxui.md" data-raw-source="[&lt;strong&gt;messageBoxUI&lt;/strong&gt;](messageboxui.md)"><strong>messageBoxUI</strong></a></p></td>
<td><p></p>
<p>一个可选元素，用于在客户端计算机上显示消息框。</p></td>
</tr>
</tbody>
</table>

## <a name="examples"></a>示例

下面的代码示例演示如何使用 **bitmap** 元素。

```xml
<?xml version="1.0" ?>
   <asyncPrintUIRequest xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/request">
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

## <a name="see-also"></a>请参阅

[**messageBoxUI**](messageboxui.md)
