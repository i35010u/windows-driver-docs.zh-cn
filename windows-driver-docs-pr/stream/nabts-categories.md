---
title: NABTS 类别
description: NABTS 类别
keywords:
- 流类别 WDK 视频捕获，NABTS
- PINNAME_VIDEO_NABTS
- 北美广播 Teletext 标准 WDK 视频捕获
- NABTS WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2c80cbff509cd0e7ec9bc7c22dc84449daef841
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795271"
---
# <a name="nabts-categories"></a>NABTS 类别


以下 GUID 对应于北美广播 Teletext Standard (NABTS) 类别：

-   **PINNAME \_ VIDEO \_ NABTS**

    北美广播 Teletext 标准 (NABTS) 类别输出插针提供解码的原始或转发错误更正流 (FEC) NABTS 数据。

Raw 或 FEC NABTS data 的唯一区别在于 SubFormat GUID 的值

指定 **PINNAME \_ VIDEO \_ NABTS** pin 时，使用下表中列出的信息。

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
<td><p>KSDATAFORMAT_SUBTYPE_NABTS (raw NABTS) </p>
<p>KSDATAFORMAT_SUBTYPE_NABTS_FEC (向前纠错 NABTS) </p></td>
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
<td><p>MEDIATYPE_VBI</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>FORMAT_VBI</p></td>
</tr>
</tbody>
</table>

 

 

 




