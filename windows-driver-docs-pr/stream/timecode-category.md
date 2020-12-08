---
title: 时间码类别
description: 时间码类别
keywords:
- 流类别 WDK 视频捕获，imecode
- 时间码类别 WDK 视频捕获
- PINNAME_VIDEO_TIMECODE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 718ca913341d0048d2b9613eaccac2825cc64ac3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782001"
---
# <a name="timecode-category"></a>时间码类别


以下 GUID 对应于时间码类别：

-   **PINNAME \_ 视频时间 \_ 码**

    时间码类别输出插针提供时间码流。

创建 **PINNAME \_ 视频时间 \_ 码** pin 时，请使用下表中列出的信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DataRange 结构</strong></p></td>
<td><p>KSDATARANGE</p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 结构</strong></p></td>
<td><p>KSDATAFORMAT</p></td>
</tr>
<tr class="odd">
<td><p><strong>主要格式 GUID</strong></p></td>
<td><p>未定义。 使用 "直接显示的 MEDIATYPE_Timecode" 定义 GUID。</p></td>
</tr>
<tr class="even">
<td><p><strong>子格式 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_NONE</p></td>
</tr>
<tr class="odd">
<td><p><strong>说明符 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NONE</p></td>
</tr>
<tr class="even">
<td><p><strong>扩展的标头大小</strong></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>必需的属性集</strong></p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p><strong>必需的事件集</strong></p></td>
<td><p>无</p></td>
</tr>
<tr class="odd">
<td><p><strong>DirectShow majortype</strong></p></td>
<td><p>MEDIATYPE_Timecode</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>MEDIASUBTYPE_None</p></td>
</tr>
</tbody>
</table>

 

 

 




