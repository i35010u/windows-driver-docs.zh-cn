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
ms.openlocfilehash: f396a781e8a1e4fe9dd11fc66c9c53c7227ffa45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523796"
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
<th>属性</th>
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
<td><p>未定义任何内容。 定义使用直接显示的 GUID&#39;s MEDIATYPE_Timecode。</p></td>
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

 

 

 




