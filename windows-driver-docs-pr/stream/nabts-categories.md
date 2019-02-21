---
title: NABTS 类别
description: NABTS 类别
ms.assetid: 7d064ed4-1bd9-4457-83c8-8b1fee10251c
keywords:
- 流类别 WDK 视频捕获 NABTS
- PINNAME_VIDEO_NABTS
- North American 广播 Teletext 标准 WDK 视频捕获
- NABTS WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70ab8fb0b906e12c40432a1128e2a257cb008720
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522632"
---
# <a name="nabts-categories"></a>NABTS 类别


以下 GUID 对应于 North American 广播 Teletext 标准 (NABTS) 类别：

-   **PINNAME\_VIDEO\_NABTS**

    输出插针，North American 广播 Teletext 标准 (NABTS) 类别提供的原始解码的流或转发错误更正 (FEC) NABTS 数据。

原始之间的唯一区别或 FEC NABTS 数据为的子格式 GUID 值

指定时**PINNAME\_视频\_NABTS**插针，使用下表中列出的信息。

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
<td><p>KS_DATARANGE</p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 结构</strong></p></td>
<td><p>KS_DATAFORMAT</p></td>
</tr>
<tr class="odd">
<td><p><strong>主要格式 GUID</strong></p></td>
<td><p>KS_DATAFORMAT_TYPE_NABTS</p></td>
</tr>
<tr class="even">
<td><p><strong>SubFormat GUID</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_NABTS (原始 NABTS)</p>
<p>KSDATAFORMAT_SUBTYPE_NABTS_FEC （前向纠错 NABTS）</p></td>
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
<td><p>MEDIATYPE_VBI</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>FORMAT_VBI</p></td>
</tr>
</tbody>
</table>

 

 

 




