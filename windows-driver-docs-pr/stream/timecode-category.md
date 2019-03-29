---
title: 时间码类别
description: 时间码类别
ms.assetid: 273e0233-357e-4e13-bf8e-77ca36834ee7
keywords:
- 流类别 WDK 视频捕获 imecode
- 时间码类别 WDK 视频捕获
- PINNAME_VIDEO_TIMECODE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00abaa1cc92b55dffb86b151b56023303d65341e
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350124"
---
# <a name="timecode-category"></a>时间码类别


以下 GUID 对应于时间码类别：

-   **PINNAME\_视频\_时间代码**

    输出插针，时间码类别提供时间码的流。

创建时**PINNAME\_视频\_时间码**插针，使用下表中列出的信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特性</th>
<th>ReplTest1</th>
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
<td><p>未定义任何内容。 定义使用直接显示的 MEDIATYPE_Timecode 的 GUID。</p></td>
</tr>
<tr class="even">
<td><p><strong>子设置的 GUID 格式</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_NONE</p></td>
</tr>
<tr class="odd">
<td><p><strong>说明符 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NONE</p></td>
</tr>
<tr class="even">
<td><p><strong>扩展标头大小</strong></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>所需的属性集</strong></p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p><strong>所需的事件集</strong></p></td>
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

 

 

 




